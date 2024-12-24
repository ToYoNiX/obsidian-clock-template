
```dataviewjs
// Create a container div for the clock widget
const clockDiv = this.container.createDiv({ cls: "clock-widget" });

// Inject HTML structure after the container is created
clockDiv.innerHTML = `
  <div style="text-align: center;">
      <h1 id="clock-time" style="font-size: 3em; margin: 0;">Loading...</h1>
      <p id="clock-date" style="margin: 0; color: gray;">Loading...</p>
  </div>
`;

// Cache the clock and date elements outside the update function for performance
const clockElement = clockDiv.querySelector("#clock-time");
const dateElement = clockDiv.querySelector("#clock-date");

// JavaScript function to update the clock and date
function updateClock() {
  const now = new Date();
  
  // Specify options to use the 24-hour format (hour12: false)
  const timeString = now.toLocaleTimeString([], {
    hour: '2-digit',
    minute: '2-digit',
    second: '2-digit',
    hour12: false // Use 24-hour format
  });

  // Manually format the date as DD/MM/YYYY
  const day = String(now.getDate()).padStart(2, '0'); // Ensure two digits
  const month = String(now.getMonth() + 1).padStart(2, '0'); // Months are zero-indexed
  const year = now.getFullYear();
  const dateString = `${day}/${month}/${year}`; // Format the date

  // Update the content of the clock and date directly
  if (clockElement) {
    clockElement.textContent = timeString;
  }
  if (dateElement) {
    dateElement.textContent = dateString;
  }

  // Schedule the next update
  requestAnimationFrame(updateClock);
}

// Start updating the clock
updateClock();
```
