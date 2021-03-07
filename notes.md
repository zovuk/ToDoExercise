1. CHANGE ---------------------- BUG

“One bug is a simple typo.”
Controler.prototype adddItem had to many d`s.

2. CHANGE ---------------------- BUG

“One bug involves an introduction of potential conflict between duplicate IDs.”
In store.js where is ID generated there was a possibility to generate an ID that already exists. I made the ID bigger and included a loop that checks newly given ID to be unique.

store.js

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

3. CHANGE ---------------------- IMPROVEMENT

Newest item added on the top of the list instead on the bottom for better UI experience.

4. CHANGE ---------------------- IMPROVEMENT

In node_modules/todomvc-common/base.js following line in code is commented cause it was calling file that does not exist. In console was trowing error: "GET http://127.0.0.1:5500/learn.json 404 (Not Found)"

    248 getFile('learn.json', Learn);

5. CHANGE ---------------------- BUG (maybe) (not fixed)

There is (maybe) a bug that gives this error in console when URL have fragments:
"Autofocus processing was blocked because a document's URL has a fragment '#/'."
Same is for fragments in URL '#/active' or '#/completed'. This happening when user refresh the site after fragment is added in its URL. Page was supposed to autofocus on the input field for new ToDo.

I searched how to fix this but it turned out that it is about HTML it self and that many does not even consider it as a bug. For example how they talk about it on WHATWG.org.
https://github.com/whatwg/html/issues/5252

But I did found a way to make it work in a way that after refreshing application always returns at the first page without fragments as it is loaded for the first time:

app.js

    // $on(window, 'load', setView);
    // ZORAN - remove fragments from URL
    $on(window, 'load', () => {
      if (window.performance.getEntriesByType('navigation')) {
        if (
          window.performance.getEntriesByType('navigation')[0].type === 'reload'
        ) {
          document.location.href = String(document.location.href).replace(
            /#\/(.*)/,
            ''
          );
        }
      }
      setView();
    });
    // END - remove fragments from URL
