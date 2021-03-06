## 1) Add the following to styles.css
```
body {
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
}

.topnav {
    overflow: hidden;
    background-color: darkslategrey;
}

.topnav a {
    float: left;
    color: #f2f2f2;
    text-align: center;
    padding: 14px 16px;
    text-decoration: none;
    font-size: 17px;
}

.topnav a:hover {
    background-color: #ddd;
    color: black;
}

.topnav a.active {
    background-color: lightskyblue;
    color: white;
}
```
### 2) Create a new file `bookRepository.js` (in the root of the project) and add the following content to the file
```
function bookRepository() {
  let books = [
    { id: 100, title: "How to Learn JavaScript - Vol 1", info: "Study hard" },
    { id: 101, title: "How to Learn ES6..", info: "Complete all exercises :-)" },
    { id: 102, title: "How to Learn Client Side Routing", info: "Complete all your Exercises" },
    { id: 103, title: "How to Learn it all", info: "Don't drink beer(s), until Friday (after four)" }
  ]
  let nextId = 104;

  const getBooks = () => { return books }

  const findBook = (id) => {
    const bookId = isNaN(id) ? id : Number(id);
    return books.find(book => book.id === bookId)
  }

  const deleteBook = (id) => {
    const bookId = Number(id)
    books = books.filter(book => book.id !== bookId)
  }

  const addBook = (book) => {
    book.id = nextId
    books.push(book)
    nextId++;
    return book
  }

  const editBook = (book, id) => {
    const bookToEdit = findBook(id)
    bookToEdit.title = book.title
    bookToEdit.info = book.info;
    return bookToEdit
  }

  return {
    // Remember all statements below are a shortcut for this version: getBooks: getBooks
    getBooks,
    findBook,
    deleteBook,
    addBook,
    editBook,
  }
}

/*************************************************************************************** 
  This part is for when you start to talk with an API
  Taken from this document: https://docs.google.com/document/d/1keZvtIhEb7qFpa4LblPJLKETy1CskAf5GP4XczqaN-0/edit#bookmark=id.j1nnjw6ga7ru 
****************************************************************************************/   

const URL = "http://localhost:3000/books"
function makeOptions(method, body) {
  const opts = {
    method: method,
    headers: {
      "Content-type": "application/json",
      "Accept": "application/json"
    }
  }
  if (body) { //Observe how we can add new fields to an object when needed
    opts.body = JSON.stringify(body);
  }
  return opts;
}

export default bookRepository();
```
