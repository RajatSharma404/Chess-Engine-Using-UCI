# Chess Engine Using UCI

A chess engine written in **C# (.NET 9)** that communicates over the **Universal Chess Interface (UCI)** protocol. The engine is named **Cheese** and is built to be plugged into any UCI-compatible chess GUI.

---

## What is UCI?

The **Universal Chess Interface** (UCI) is an open communication protocol that allows chess engines to interact with graphical interfaces (GUIs) or other programs. It works over standard input/output (stdin/stdout), making integration straightforward and GUI-agnostic.

Popular UCI-compatible GUIs include:

- [Arena Chess GUI](http://www.playwitharena.de/)
- [Cute Chess](https://cutechess.com/)
- [Lucas Chess](https://lucaschess.pythonanywhere.com/)
- [Scid vs. PC](http://scidvspc.sourceforge.net/)

---

## Project Structure

```
Chess-Engine-Using-UCI/
├── Program.cs          # Entry point — starts the UCI loop
├── UCI.cs              # UCI protocol handler (uci, isready, position, go, quit)
├── Board.cs            # Board representation
├── Piece.cs            # Piece definitions
├── Move.cs             # Move representation
├── Engine.cs           # Search algorithm
├── Evaluation.cs       # Position evaluation
├── Utils.cs            # Shared utility functions
└── Chess-Engine-Using UCI.csproj
```

| File            | Responsibility                                                  |
| --------------- | --------------------------------------------------------------- |
| `UCI.cs`        | Reads UCI commands from stdin, dispatches to handlers           |
| `Board.cs`      | Stores and updates the board state (pieces, side to move, etc.) |
| `Piece.cs`      | Defines piece types and colours                                 |
| `Move.cs`       | Encodes a chess move (from, to, promotion, flags)               |
| `Engine.cs`     | Implements the search (minimax / alpha-beta)                    |
| `Evaluation.cs` | Scores a position (material, piece-square tables, etc.)         |
| `Utils.cs`      | Helper functions shared across modules                          |

---

## Supported UCI Commands

| Command    | Status         | Description                               |
| ---------- | -------------- | ----------------------------------------- |
| `uci`      | ✅             | Responds with engine identity and `uciok` |
| `isready`  | ✅             | Responds with `readyok`                   |
| `position` | 🚧 In progress | Parses start position and move list       |
| `go`       | 🚧 In progress | Starts the search and returns `bestmove`  |
| `quit`     | ✅             | Exits the engine cleanly                  |

---

## Prerequisites

- [.NET 9 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/9.0)

Check your installation:

```bash
dotnet --version
```

---

## Build & Run

**Clone the repository:**

```bash
git clone https://github.com/MuditAtrey/Chess-Engine-Using-UCI.git
cd Chess-Engine-Using-UCI
```

**Build:**

```bash
dotnet build
```

**Run directly:**

```bash
dotnet run
```

Once running, the engine listens for UCI commands on stdin. You can type commands manually to test it:

```
uci
isready
quit
```

**Build a standalone executable:**

```bash
dotnet publish -c Release -r win-x64 --self-contained true
```

The binary will be output to `bin/Release/net9.0/win-x64/publish/`.

---

## Connecting to a GUI

1. Build the project (see above) or use `dotnet run` via a wrapper script.
2. Open your UCI-compatible GUI (e.g., Arena).
3. Navigate to **Engines → Install New Engine** (exact menu name depends on your GUI).
4. Point it to the compiled `.exe` (or the `dotnet run` wrapper).
5. The GUI will issue `uci` and your engine will respond — you're ready to play!

---

## Roadmap

- [ ] Complete board state parsing (`position` command)
- [ ] Implement legal move generation
- [ ] Implement minimax search with alpha-beta pruning
- [ ] Add basic material evaluation
- [ ] Add piece-square table evaluation
- [ ] Support time controls (`go movetime`, `go wtime btime`)
- [ ] Add opening book support
- [ ] Iterative deepening

---

## Contributing

Pull requests are welcome! If you'd like to contribute:

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/your-feature-name`
3. Commit your changes: `git commit -m "Add your feature"`
4. Push to your fork: `git push origin feature/your-feature-name`
5. Open a Pull Request against `main`.

---

## Author

**Mudit Atrey** — [@MuditAtrey](https://github.com/MuditAtrey)
