# Eastvantage
Project
Install all the necessary dependencies like
import React, { useState, useEffect } from 'react';
import axios from 'axios'; 
at the start of the app i.e app.js in src folder

Use the useState hooks and useEffect for the proper execution:-
const UserDisplay = () => {
  const [userData, setUserData] = useState({ fullName: '', email: '' });

write a function for fetching user data and save it to local storage
  const fetchAndSaveUserData = async () => {
    try {
      const response = await axios.get('https://randomuser.me/api');
      const user = response.data.results[0];
      const { name, email } = user;
      const fullName = `${name.first} ${name.last}`;
      setUserData({ fullName, email });
Use the useEffect hook nowto fetch the data:-

      // Save the data to local storage
      localStorage.setItem('userData', JSON.stringify({ fullName, email }));
    } catch (error) {
      console.error('Error fetching data:', error);
    }
  };

  // Function to handle the Refresh button click
  const handleRefresh = () => {
    fetchAndSaveUserData();
  };

  useEffect(() => {
    // Check if the data is already in local storage and use it if available
    const storedUserData = localStorage.getItem('userData');
    if (storedUserData) {
      const { fullName, email } = JSON.parse(storedUserData);
      setUserData({ fullName, email });
    } else {
      fetchAndSaveUserData();
    }
  }, []);

  Now render and return the function 
    return (
    <div>
      <h1>User Information</h1>
      <p>Full Name: {userData.fullName}</p>
      <p>Email Address: {userData.email}</p>
      <button onClick={handleRefresh}>Refresh</button>
    </div>
  );
};

function App() {
  return (
    <div className="App">
      <UserDisplay />
    </div>
  );
}

export default App;


  
