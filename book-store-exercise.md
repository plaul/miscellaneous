## 1) Add the following to styles.css (leave styles for body)
```
ul.header {
  list-style-type: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
  background-color: #333;
 }
 
 ul.header li { float: left;}
 
 ul.header li a {
  display: block;
  color: white;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
 }
 ul.header li a:hover:not(.active) { background-color: #111;}
 .active { background-color: #4CAF50;}
 ```
### 2) Create a new file bookRepository.js and add the following content to the file
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
export default bookRepository();
```


3) In index.js remove EVERYTHING below import App from "./App" and add this code
import bookFacade from "./bookFacade";
import { BrowserRouter as Router } from "react-router-dom";

const AppWithRouter = () => {
  return (
    <Router>
      <App bookFacade={bookFacade} />
    </Router>
  );
};
ReactDOM.render(<AppWithRouter />, document.getElementById("root"));
