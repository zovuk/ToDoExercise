### **1. CHANGE ---------------------- BUG**

---

&nbsp;

> “One bug is a simple typo.”

In controller.js .adddItem have to many d`s.

&nbsp;

controller.js

```JavaScript
Controller.prototype.addItem = function...
```

&nbsp;

&nbsp;

### **2. CHANGE ---------------------- BUG**

---

&nbsp;

> “One bug involves an introduction of potential conflict between duplicate IDs.”

In store.js where is ID generated there was a possibility to generate an ID that already exists. I made the ID bigger and included a loop that checks newly given ID to be unique.

&nbsp;

store.js

```JavaScript
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
```

&nbsp;

&nbsp;

### **3. CHANGE ---------------------- IMPROVEMENT**

---

&nbsp;

Newest item added on the top of the list instead on the bottom for better UI experience.

&nbsp;

store.js

```JavaScript
// ZORAN - 'todos.push' replaced with 'todos.unshift' for newest item to be added at the top of the list
todos.unshift(updateData);
```

&nbsp;

&nbsp;

### **4. CHANGE ---------------------- IMPROVEMENT**

---

&nbsp;

Following line in code is commented cause it was calling file that does not exist.

&nbsp;

node_modules/todomvc-common/base.js

```JavaScript
248 getFile('learn.json', Learn);
```

In console was trowing error:

```
GET http://127.0.0.1:5500/learn.json 404 (Not Found)
```

&nbsp;

&nbsp;

### **5. CHANGE ---------------------- BUG**

---

&nbsp;

There is (maybe) a bug that gives this error in console when URL have fragments:
"Autofocus processing was blocked because a document's URL has a fragment '#/'."
Same is for fragments in URL '#/active' or '#/completed'. This happening when user refresh the site after fragment is added in its URL. Page was supposed to autofocus on the input field for new ToDo.

I searched how to fix this but it turned out that it is about HTML it self and that many does not even consider it as a bug. For example how they talk about it on [WHATWG.org](https://github.com/whatwg/html/issues/5252).

But I did found a way to make it work in a way that after refreshing application always returns at the first page without fragments as it is loaded for the first time:

&nbsp;

app.js

```JavaScript
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
```

&nbsp;

&nbsp;

### **6. QUESTION ----------------------**

---

&nbsp;

With this one I am little bit confused. For test is said "should check the toggle all button, if all todos are completed" and that should mean if user marks every todo item as completed the toggle all button would be checked, but Controller method .toggleAll read all active todo's and changing their status to completed what actually is action of the button that changes all active todo's to completed.

&nbsp;

ControllerSpec.js

```JavaScript
it('should check the toggle all button, if all todos are completed', function () {
  setUpModel([{ title: 'my todo', completed: true }]);
  subject.setView('');
  expect(view.render).toHaveBeenCalledWith('toggleAll', {
    checked: true,
  });
});
```

controller.js

```JavaScript
/**
* Will toggle ALL checkboxes' on/off state and completeness of models.
* Just pass in the event object.
*/
Controller.prototype.toggleAll = function (completed) {
  var self = this;
  self.model.read({ completed: !completed }, function (data) {
    data.forEach(function (item) {
      self.toggleComplete(item.id, completed, true);
    });
  });
  self._filter();
};
```

&nbsp;

&nbsp;

### **7. CHANGE ---------------------- BUG**

---

&nbsp;

Toggle All Button was not working. I needed to change position and size in index.css to make it work.

node_modules\todomvc-app-css\index.css

```CSS
.toggle-all {
	width: 40px; /* ZORAN - changed */
	height: 60px; /* ZORAN - changed */
	border: none; /* Mobile Safari */
	opacity: 0;
	position: absolute;
	top: -60px; /* ZORAN - changed */
	/* left: -13px; */ /* ZORAN - changed */
	z-index: 999; /* ZORAN - added */
}
```
