// inicializa o firebase
firebase.initializeApp(firebaseConfig);

// referencia ao nó "mensagens"
const messagesRef = firebase.database().ref('mensagens');

// envia uma nova mensagem
function sendMessage(message) {
  messagesRef.push().set({
    message: message,
    timestamp: firebase.database.ServerValue.TIMESTAMP
  });
}

// recebe novas mensagens em tempo real
messagesRef.on('child_added', function(snapshot) {
  const message = snapshot.val();
  console.log('Nova mensagem:', message.message);
});
