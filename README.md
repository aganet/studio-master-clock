# LED Masterclock with NTP Sync

A fullscreen LED-style masterclock that dynamically displays the current time, synchronizes with an NTP server, and highlights second segments with an interactive visual effect.

![master-clock](https://github.com/user-attachments/assets/877a2fba-d43a-4280-a8dc-6d10175b1404)


## Features

- **Fullscreen LED Clock**: Displays the current time in an LED-style layout.
- **Dynamic Segment Highlighting**: Segments light up to indicate seconds passed.
- **Customizable Text**: Add a custom message, such as a ham radio call sign, below the clock.
- **NTP Synchronization**: Fetches time from an NTP server and displays synchronization status along with the time difference.
- **Responsive Design**: Automatically adjusts to any screen size for an optimal experience.

## Demo

[DEMO](https://aganet.gr/clock/)


## Installation

1. Clone the repository or download the project:
   ```bash
   git clone https://github.com/your-username/led-masterclock.git
   cd led-masterclock
   ```

2. Open the `index.html` file in a browser to view the clock:
   ```bash
   open index.html
   ```

## Customization

### Changing the Custom Text
To change the custom text displayed below the clock (e.g., your call sign):

1. Open the `index.html` file.
2. Locate the `customText` variable in the script:
   ```javascript
   let customText = "M0JPK"; // Replace with your text
   ```
3. Update the text to your desired value.

### Adjusting the Design
Modify the `style` section in the `index.html` file to change the layout, colors, or sizes.

## How It Works

- **Clock Rendering**: The clock uses the `Date` object to fetch the local time from the user's system and dynamically updates the time display and segment highlights every second.
- **NTP Sync**: Synchronizes with the [WorldTimeAPI](https://worldtimeapi.org/) to ensure accuracy. The time difference between the system clock and the NTP server is displayed in the top-left corner.
- **Precise Timing**: Uses `setTimeout` to synchronize updates with the system clock.

## Requirements

- A modern web browser (Google Chrome, Firefox, Edge, Safari, etc.)
- Internet connection (required for NTP synchronization)

## Contributing

Contributions are welcome! To contribute:

1. Fork the repository.
2. Create a feature branch:
   ```bash
   git checkout -b my-feature-branch
   ```
3. Commit your changes:
   ```bash
   git commit -m "Add new feature"
   ```
4. Push your branch:
   ```bash
   git push origin my-feature-branch
   ```
5. Open a Pull Request.

## License

This project is licensed under the [MIT License](LICENSE).

## Credits

- **WorldTimeAPI** for providing free NTP synchronization.
- The open-source community for inspiration and contributions.

---

You can directly save this response as `README.md` in your project repository. Let me know if you need further changes!
