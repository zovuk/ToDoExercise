1. CHANGE ----------------------

“One bug is a simple typo.”
Controler.prototype adddItem had to many d`s.

2. CHANGE ----------------------

“One bug involves an introduction of potential conflict between duplicate IDs.”
In store.js where is ID generated there was a possibility to generate an ID that already exists. I made the ID bigger and included a loop that checks newly given ID to be unique.

    // Generate an ID
    var newId = '';
    var charset = '0123456789';

    // changed ID number size from 6 to 9 to have much more variations
    for (var i = 0; i < 9; i++) {
      newId += charset.charAt(Math.floor(Math.random() * charset.length));
    }

    // this loop added to make every new ID unique
    if (todos.find((e) => e.id === Number(newId))) {
      while (todos.find((e) => e.id === Number(newId))) {
        var newId = '';
        for (var i = 0; i < 6; i++) {
          newId += charset.charAt(Math.floor(Math.random() * charset.length));
        }
      }
    }

3. CHANGE ----------------------

Newest item added on the top of the list instead on the bottom for better UI experience.
