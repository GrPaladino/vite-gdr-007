# This is our version of your Street Fighter-style combat game web app developed with Vue.js. Here’s how it works:

- Character Selection:

  - Users choose a character from the list provided.
  - The app retrieves this list via an Axios call to the database.

- CPU Selection:

  - After the user selects their character, the CPU randomly chooses one.
  - The game begins once both characters are selected.

- Gameplay Mechanics:

  - When the “Play” button is pressed:
  - The user’s character launches an attack.
  - Immediately afterward, the CPU’s character counterattacks.
  - The game logic compares attack points with defense points.
  - If the difference is positive, the attacked character loses HP (equal to the difference).
  - If the difference is negative, the attacking character loses HP (equal to the difference).
  - The game continues until one character’s HP reaches 0.

  ## Screen

  ![screen](/public/img/screen1.jpg)

  ![screen](/public/img/screen2.jpg)

  ![screen](/public/img/screen3.jpg)

  ![screen](/public/img/screen4.jpg)
