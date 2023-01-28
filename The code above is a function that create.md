The code above is a function that creates a dialog box. The dialog box has a title, a message, and two buttons. The first button is labeled "OK" and the second button is labeled "Cancel". When the user clicks the "OK" button, the dialog box closes. When the user clicks the "Cancel" button, the dialog box closes.


        favDialog.showModal();
      }
    }
  });

  // Add to homescreen code
  var deferredPrompt;

  window.addEventListener('beforeinstallprompt', function(e) {
    // Prevent Chrome 67 and earlier from automatically showing the prompt
    e.preventDefault();
    // Stash the event so it can be triggered later on the button event.
    deferredPrompt = e;

    showAddToHomeScreen();

  });

  function showAddToHomeScreen() {  
    var a2hsBtn = document.querySelector(".ad2hs-prompt");  

    a2hsBtn.style.display = "block";  

    a2hsBtn.addEventListener("click", addToHomeScreen);  
  }  

  function addToHomeScreen() {  
    var a2hsBtn = document.querySelector(".ad2hs-prompt");  
    // hide our user interface that shows our A2HS button  
    a2hsBtn.style.display = 'none';  
    // Show the prompt  
    deferredPrompt.prompt();  
    // Wait for the user to respond to the prompt  
    deferredPrompt.userChoice  
      .then(function(choiceResult) {  
        if (choiceResult.outcome === 'accepted') {  
          console.log('User accepted the A2HS prompt');  
        } else {  
          console.log('User dismissed the A2HS prompt');  
        }