# Spinix

Spinix 🌀 is a Go package that provides terminal-based loading animations, including spinners and progress bars. It supports customizable themes, colors, and speeds, allowing developers to create visually appealing loading indicators that can fit various terminal environments and aesthetics.

## Features

- **Spinners**: Multiple spinner styles with customizable speed and colors.
- **Progress Bars**: A customizable progress bar with adjustable width, characters, and styles.
- **Thread Safety**: Safe to use in concurrent environments with mutexes.
- **Customizable Themes**: Use predefined themes or create your own custom spinner themes.

## Installation

To install Spinix, use `go get`:

```bash
go get github.com/Kei-K23/spinix
```

## Usage

### Spinners

Here’s how to create and use a spinner:

```go
package main

import (
	"time"
	"github.com/Kei-K23/spinix" // Replace with your actual import path
)

func main() {
	spinner := spinix.NewSpinner()
    .SetMessage("Loading...")
    .SetLoaderColor("\033[34m") // Blue
    .SetSpeed(100 * time.Millisecond) // Adjust speed if necessary

	spinner.Start()

	// Simulate some work
	time.Sleep(5 * time.Second)

	spinner.Stop()
}
```

### Progress Bars

Creating and using a progress bar is just as straightforward:

```go
package main

import (
	"time"
	"github.com/Kei-K23/spinix" // Replace with your actual import path
)

func main() {
	progressBar := spinix.NewProgressBar()
	.SetWidth(50)
	.SetColor("\033[32m") // Green
	.SetLabel("Progress:")
	.Start()

	for i := 0; i <= 100; i++ {
		progressBar.Update(i)
		time.Sleep(50 * time.Millisecond) // Simulate work
	}

	progressBar.Stop()
}
```

## Customization

### Spinners

You can customize the spinner’s message, colors, and theme:

```go
func main() {
	spinner := spinix.NewSpinner().
		SetMessage("Processing...").
		SetMessageColor("\033[33m").
		SetCustomTheme([]string{"🔅", "🔆", "🔅", "🔆"})

	spinner.Start()
	time.Sleep(2 * time.Second) // Simulate a task
	spinner.Stop()
}
```

### Progress Bars

You can customize the progress bar's appearance using various methods:

```go
func main() {
	progressBar := spinix.NewProgressBar().
		SetWidth(60).
		SetBarChar("█").
		SetEmptyChar("░").
		SetBorders("[", "]").
		SetShowPercentage(true)

	progressBar.Start()

	for i := 0; i <= 100; i++ {
		progressBar.Update(i)
		time.Sleep(50 * time.Millisecond) // Simulate work
	}

	progressBar.Stop()
}
```

## Use Pre-defined Spinner and Progress bar

### Spinners

You can use pre-defined spinner theme that provided by **spinix**:

```go
func main() {
	spinner := spinix.NewSpinner().
		SetMessage("Processing...").
		SetMessageColor("\033[33m").
		SetTheme(spinix.SpinnerRotatingArrow)

	spinner.Start()

	// Simulate some work
	time.Sleep(5 * time.Second)

	spinner.Stop()
}
```

### Progress Bars

You can use pre-defined progress bar style that provided by **spinix**:

```go
func main() {
	progressBar := spinix.NewProgressBar().
		SetStyle(spinix.PbStyleBasic).
		SetShowPercentage(true)

	progressBar.Start()

	for i := 0; i <= 100; i++ {
		progressBar.Update(i)
		time.Sleep(50 * time.Millisecond) // Simulate work
	}

	progressBar.Stop()
}
```

## Available Spinner Themes

The Spinix package comes with several predefined spinner themes. Here’s a list of the available styles along with their visualizations:

| Spinner Theme            | Visualization                                |
| ------------------------ | -------------------------------------------- |
| **SpinnerClassicDots**   | ⠋ ⠙ ⠹ ⠸ ⠼ ⠴ ⠦ ⠧ ⠇ ⠏                          |
| **SpinnerLineTheme**     | - \                                          |
| **SpinnerPulsatingDot**  | ⠁ ⠂ ⠄ ⠂                                      |
| **SpinnerGrowingBlock**  | ▁ ▃ ▄ ▅ ▆ ▇ █ ▇ ▆ ▅ ▄ ▃                      |
| **SpinnerRotatingArrow** | → ↘ ↓ ↙ ← ↖ ↑ ↗                              |
| **SpinnerArcLoader**     | ◜ ◠ ◝ ◞ ◡ ◟                                  |
| **SpinnerClock**         | 🕛 🕐 🕑 🕒 🕓 🕔 🕕 🕖 🕗 🕘 🕙 🕚          |
| **SpinnerCircleDots**    | ◐ ◓ ◑ ◒                                      |
| **SpinnerBouncingBall**  | ⠁ ⠂ ⠄ ⠂                                      |
| **SpinnerFadingSquares** | ▖ ▘ ▝ ▗                                      |
| **SpinnerDotsFading**    | ⠁ ⠂ ⠄ ⠂ ⠁ ⠂ ⠄ ⠂                              |
| **SpinnerEarth**         | 🌍 🌎 🌏                                     |
| **SpinnerSnake**         | ⠈ ⠐ ⠠ ⢀ ⡀ ⠄ ⠂ ⠁                              |
| **SpinnerTriangle**      | ◢ ◣ ◤ ◥                                      |
| **SpinnerSpiral**        | ▖ ▘ ▝ ▗ ▘ ▝ ▖ ▗                              |
| **SpinnerWave**          | ▁ ▂ ▃ ▄ ▅ ▆ ▇ █ ▇ ▆ ▅ ▄ ▃ ▂ ▁                |
| **SpinnerWeather**       | 🌤️ ⛅ 🌥️ ☁️ 🌧️ ⛈️ 🌩️ 🌨️                      |
| **SpinnerRunningPerson** | 🏃💨 🏃💨💨 🏃💨💨💨 🏃‍♂️💨 🏃‍♂️💨💨 🏃‍♀️💨 🏃‍♀️💨💨 |
| **SpinnerRunningCat**    | 🐱💨 🐈💨 🐱💨💨 🐈💨💨                      |
| **SpinnerRunningDog**    | 🐕💨 🐶💨 🐕‍🦺💨 🐕💨💨                        |
| **SpinnerCycling**       | 🚴 🚴‍♂️ 🚴‍♀️ 🚵 🚵‍♂️ 🚵‍♀️                            |
| **SpinnerCarLoading**    | 🚗💨 🚙💨 🚓💨 🚕💨 🚐💨 🚔💨                |
| **SpinnerRocket**        | 🚀 🚀💨 🚀💨💨 🚀💨💨💨 🚀🌌 🚀🌠            |
| **SpinnerOrbit**         | 🌑 🌒 🌓 🌔 🌕 🌖 🌗 🌘                      |
| **SpinnerTrain**         | 🚆 🚄 🚅 🚇 🚊 🚉                            |
| **SpinnerAirplane**      | ✈️ 🛫 🛬 ✈️💨 ✈️💨💨                         |
| **SpinnerFireworks**     | 🎆 🎇 🎆🎇 🎇🎆                              |
| **SpinnerPizzaDelivery** | 🍕💨 🍔💨 🌭💨 🍟💨                          |
| **SpinnerHeartbeat**     | 💓 💗 💖 💘 💞 💝 💖                         |

## Available Progress Bar Styles

The ProgressBar can be styled using various predefined styles. Here’s a list of available styles:

| Progress Bar Style    | Description                                              |
| --------------------- | -------------------------------------------------------- |
| **PbStyleBasic**      | Simple progress bar with basic characters.               |
| **PbStyleClassic**    | Classic style with borders and filled characters.        |
| **PbStyleMinimal**    | Minimalistic design with no borders.                     |
| **PbStyleBold**       | Bold characters with decorative borders.                 |
| **PbStyleDashed**     | Dashed design for a unique look.                         |
| **PbStyleElegant**    | Elegant characters and borders for a sophisticated look. |
| **PbStyleEmoji**      | Fun design using emojis for a playful effect.            |
| **PbStyleFuturistic** | Futuristic characters and borders for a modern feel.     |

## Example

Here’s a complete example that demonstrates both the spinner and the progress bar together:

```go
package main

import (
	"time"
	"github.com/Kei-K23/spinix" // Replace with your actual import path
)

func main() {
	spinner := spinix.NewSpinner()
	progressBar := spinix.NewProgressBar()

	spinner.SetMessage("Loading Data...")
	spinner.Start()
	progressBar.SetWidth(50)
	progressBar.SetColor("\033[36m") // Cyan
	progressBar.Start()

	for i := 0; i <= 100; i++ {
		progressBar.Update(i)
		time.Sleep(50 * time.Millisecond) // Simulate work
	}

	progressBar.Stop()
	spinner.Stop()
}
```

## Contributing

Contributions are welcome! Please feel free to open issues, submit pull requests, or provide feedback.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.
