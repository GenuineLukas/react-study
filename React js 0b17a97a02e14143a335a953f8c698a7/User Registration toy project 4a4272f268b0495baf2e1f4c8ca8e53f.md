# User Registration toy project

**src codes**

- components
    - UI
        - Button.js
            
            ```jsx
            import React from "react";
            
            import classes from "./Button.module.css";
            
            const Button = (props) => {
              return (
                <button
                  className={classes.button}
                  type={props.type || "button"}
                  onClick={props.onClick}
                >
                  {props.children}
                </button>
              );
            };
            
            export default Button;
            ```
            
        - Button.module.css
            
            ```css
            .button {
              font: inherit;
              border: 1px solid #317034;
              background: #317034;
              color: white;
              padding: 0.25rem 1rem;
              cursor: pointer;
            }
            
            .button:hover,
            .button:active {
              background: #568d54;
              border-color: #568d54;
            }
            
            .button:focus {
              outline: none;
            }
            ```
            
        - Card.js
            
            ```jsx
            import React from "react";
            import classes from "./Card.module.css";
            
            const Card = (props) => {
              return (
                <div className={`${classes.card} ${props.className}`}>{props.children}</div>
              );
            };
            
            export default Card;
            ```
            
        - Card.module.css
            
            ```css
            .card {
              background: white;
              box-shadow: 0 wpx 8px rgba(0, 0, 0, 0.26);
              border-radius: 10px;
            }
            ```
            
        - ErrorModal.js
            
            ```jsx
            import React from "react";
            
            import Card from "./Card";
            import Button from "./Button";
            import classes from "./ErrorModal.module.css";
            
            const ErrorModal = (props) => {
              return (
                <div>
                  <div className={classes.backdrop} onClick={props.onConfirm} />
                  <Card className={classes.modal}>
                    <header className={classes.header}>
                      <h2>{props.title}</h2>
                    </header>
                    <div className={classes.content}>
                      <p>{props.message}</p>
                    </div>
                    <footer className={classes.actions}>
                      <Button onClick={props.onConfirm}>Okay</Button>
                    </footer>
                  </Card>
                </div>
              );
            };
            
            export default ErrorModal;
            ```
            
        - ErrorModal.module.css
            
            ```css
            .backdrop {
              position: fixed;
              top: 0;
              left: 0;
              width: 100%;
              height: 100vh;
              z-index: 10;
              background: rgba(0, 0, 0, 0.75);
            }
            
            .modal {
              position: fixed;
              top: 30vh;
              left: 10%;
              width: 80%;
              z-index: 100;
              overflow: hidden;
            }
            
            .header {
              background: #4f005f;
              padding: 1rem;
            }
            
            .header h2 {
              margin: 0;
              color: white;
            }
            
            .content {
              padding: 1rem;
            }
            
            .actions {
              padding: 1rem;
              display: flex;
              justify-content: flex-end;
            }
            
            @media (min-width: 768px) {
              .modal {
                left: calc(50% - 20rem);
                width: 40rem;
              }
            }
            ```
            
    - Users
        - AddUser.js
            
            ```jsx
            import React, { useState } from "react";
            import Card from "../UI/Card";
            import classes from "./AddUser.module.css";
            import Button from "../UI/Button";
            import ErrorModal from "../UI/ErrorModal";
            
            const AddUser = (props) => {
              const [enteredUsername, setEnteredUsername] = useState("");
              const [enteredAge, setEnteredAge] = useState("");
              const [error, setError] = useState();
            
              const addUserHandler = (event) => {
                event.preventDefault();
                if (enteredUsername.trim().length === 0 || enteredAge.trim().length === 0) {
                  setError({
                    title: "Invalid input",
                    message: "Please enter a valid name and age (none-empty values)."
                  });
                  return;
                }
                //force enteredAge to be a number by putting a plus sign
                if (+enteredAge < 1) {
                  setError({
                    title: "Invalid age",
                    message: "Please enter a valid age (>0)."
                  });
                  return;
                }
                props.onAddUser(enteredUsername, enteredAge);
                setEnteredUsername("");
                setEnteredAge("");
              };
            
              const usernameChangeHandler = (event) => {
                setEnteredUsername(event.target.value);
              };
            
              const ageChangeHandler = (event) => {
                setEnteredAge(event.target.value);
              };
            
              const errorHandler = () => {
                setError(null);
              };
            
              return (
                <div>
                  {error && (
                    <ErrorModal
                      title={error.title}
                      message={error.message}
                      onConfirm={errorHandler}
                    />
                  )}
                  <Card className={classes.input}>
                    <form onSubmit={addUserHandler}>
                      <label htmlFor="username">Username</label>
                      <input
                        id="username"
                        type="text"
                        value={enteredUsername}
                        onChange={usernameChangeHandler}
                      />
                      <label htmlFor="age">Age (Years)</label>
                      <input
                        id="age"
                        type="number"
                        value={enteredAge}
                        onChange={ageChangeHandler}
                      />
                      <Button type="submit">Add user</Button>
                    </form>
                  </Card>
                </div>
              );
            };
            
            export default AddUser;
            ```
            
        - AddUser.module.css
            
            ```css
            .input {
              margin: 2rem auto;
              padding: 1rem;
              width: 90%;
              max-width: 40rem;
            }
            
            .input label {
              display: block;
              font-weight: bold;
              margin-bottom: 0.5rem;
            }
            
            .input input {
              font: inherit;
              display: block;
              width: 100%;
              border: 1px solid #ccc;
              padding: 0.15rem;
              margin-bottom: 0.5rem;
            }
            
            .input input:focus {
              outline: none;
              border-color: #4f005f;
            }
            ```
            
        - UserList.js
            
            ```jsx
            import React from "react";
            import Card from "../UI/Card";
            import classes from "./UsersList.module.css";
            
            const UsersList = (props) => {
              //map() executes a function on every element of an array
              return (
                <Card className={classes.users}>
                  <ul>
                    {props.users.map((user) => (
                      <li key={user.id}>
                        {user.name} ({user.age} years old)
                      </li>
                    ))}
                  </ul>
                </Card>
              );
            };
            
            export default UsersList;
            ```
            
        - UserList.module.css
            
            ```css
            .users {
              margin: 3rem auto;
              width: 90%;
              max-width: 40rem;
            }
            
            .users ul {
              list-style: none;
              padding: 1rem;
            }
            
            .users li {
              border: 1px solid #ccc;
              margin: 0.5rem 0;
              padding: 0.5rem;
            }
            ```
            
- App.js
    
    ```jsx
    import React, { useState } from "react";
    import "./styles.css";
    import AddUser from "./components/Users/AddUser";
    import UsersList from "./components/Users/UsersList";
    
    function App() {
      const [usersList, setUsersList] = useState([]);
    
      const addUserHandler = (uName, uAge) => {
        setUsersList((prevUsersList) => {
          return [
            ...prevUsersList,
            { name: uName, age: uAge, id: Math.random().toString() }
          ];
        });
      };
    
      return (
        <div className="App">
          <AddUser onAddUser={addUserHandler} />
          <UsersList users={usersList} />
        </div>
      );
    }
    
    export default App;
    ```
    
- index.js
    
    ```jsx
    import { StrictMode } from "react";
    import { createRoot } from "react-dom/client";
    
    import App from "./App";
    
    const rootElement = document.getElementById("root");
    const root = createRoot(rootElement);
    
    root.render(
      <StrictMode>
        <App />
      </StrictMode>
    );
    ```
    
- styles.css
    
    ```css
    * {
      box-sizing: border-box;
    }
    
    html {
      font-family: sans-serif;
      background: #1f1f1f;
    }
    
    body {
      margin: 0;
    }
    ```