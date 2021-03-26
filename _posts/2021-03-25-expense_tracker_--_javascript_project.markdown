---
layout: post
title:      "Expense Tracker -- JavaScript Project"
date:       2021-03-25 23:53:46 -0400
permalink:  expense_tracker_--_javascript_project
---


I had a great learning experience building out this project, and here, I would like to share some of it with it you all.

After planning out the models and associations, I started with building out a basic wireframe for my application.
I also wrote out an example of the json data that I wanted to end up with, when rendering. This gave me a nice visual representation of what direction I was heading towards with my expense tracker api, and kept me on track.

The project setup seemed pretty straight forward. I was able to get it up pretty quickly. After that, I started bulilding out the rest of the api, and my frontend **vertically**, one step at a time, as encouraged in the project instructions.

For my frontend, I have 3 classes:

1)  **class Transaction** -- This class converts all transactions returned in the form of json to JavaScript Objects. This is very helpful, as now, I am able to attach methods on to my JavaScript Transaction Objects such as follows:

```
class Transaction {
    constructor(transaction) {
	  this.description: transaction.description;
	  this.amount: transaction.amount;
	  this.kind: transaction.kind;
	}
	
	static findByID(id) {
	  return this.all.find(transaction => transaction.id === id);
	}
	
	insertUpdateFormData() {
	  document.getElementByID('edit-form').setAttribute('data-id', this.id);
	  doument.getelementByID('edit-description').value = this.description;
	  ........................
	  .....................................
	}
}
```

2) **class Adapter**: Although this was not a requirement, I decided to try out the adpater pattern. This was a great refactor. This class aids in abstracting away the bit and bytes of fetching data from your index.js and into this class. With this class implemented, I can then use the `findByID` method from the **Transaction** class to find the transaction, and construct the data needed to send **PATCH** and **DELETE** fetch requests for a transaction to our backend.

3) **class App** -- This class is where most of the functionality of the application lies. All the Event Listeners for the app are defined in here, and most of the functions necessary to run the application are also defined in here.
After creating this class, I can iniliaze a new instance of the **App** class in my `index.js` file when the DOM has completed loading. I then call the function to attatch all the Event Listeners to the respective nodes, and the function to fetch all the existing transactions from the backend, and create new instances of them like so:

```
document.addEventListener('DOMContentLoaded', () => {
  const app = new App();
	
  app.attatchEventListeners();
  app.createTransactions();
}
```




