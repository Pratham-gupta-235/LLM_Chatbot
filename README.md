# RustyBot

An open-source chatbot powered by a **large language model (LLM)**, deployed using an ICP (Internet Computer Protocol) smart contract. RustyBot supports natural language conversations and is designed to be extensible and privacy-centric.

## Features

- **Smart contract backend**: Written in Rust, deployed as an ICP canister.
- **Interactive LLM chatbot**: Uses locally served, open LLM (via Ollama) for prompt completion.
- **Web-based frontend**: Built with React for a seamless, user-friendly interface.
- **Secure and extensible**: Easily migrate between ICP Ninja deployments and local environments.

## Project Structure

```
rustybot/
├── backend/
│   ├── Cargo.toml
│   └── src/
│       └── lib.rs    # Main Rust smart contract logic
├── frontend/
│   └── 
├── README.md
```

- **backend/**: Rust-based ICP smart contract (canister).
    - `Cargo.toml`: Project dependencies and crate info.
    - `src/lib.rs`: Main smart contract logic and public interface.
- **frontend/**: React code for the chatbot user interface.

## Getting Started

### 1. Quick Mainnet Deployment (via ICP Ninja)

- Open the project in [ICP Ninja](https://icp.ninja).
- Click **Deploy** (top-right) for one-click deployment to the Internet Computer mainnet.
- (Optional) Use the built-in Remix-like editor for instant browser-side changes.

### 2. Local Development & Running

**Clone or Download:**
- From ICP Ninja, press "Download files" (upper left menu) to get a zip of your project.

**Backend:**

- Make sure [Rust](https://rustup.rs/) and [dfx (DFINITY SDK)](https://smartcontracts.org/docs/quickstart/quickstart.html) are installed.

```bash
cd backend
dfx start --background
dfx deploy
```

**Frontend:**

- Requires [Node.js](https://nodejs.org/) and npm.

```bash
cd frontend
npm install
npm start
```

**Running Local LLM Service (Ollama):**

1. **Install [Ollama](https://ollama.com/):**
2. Start the Ollama server:

    ```bash
    ollama serve
    # Starts on localhost:11434
    ```

3. In a new terminal, pull and prepare the LLM:

    ```bash
    ollama run llama3.1:8b
    # Downloads the 8B Llama model (~4GiB)
    ```

## Usage

- Open your browser at [http://localhost:3000](http://localhost:3000).
- Type a prompt in the chat window and get a response!
- For mainnet: Use the auto-generated ICP Ninja frontend link after deployment.

## Architecture & Flow

1. **Frontend** (React): Presents the user chat interface and sends prompt requests.
2. **ICP Canister** (Rust): Receives prompts from frontend, forwards them to the local LLM service, and returns responses.
3. **Ollama LLM Service**: Locally processes prompts using the specified Llama model.

> **Sequence:**  
> User → Frontend → (HTTP/ICP call) → Canister → (API) → Ollama LLM → Canister → Frontend

## Troubleshooting

- **LLM not responding**: Ensure `ollama serve` is running and the model (`llama3.1:8b`) is downloaded.
- **ICP deployment issues**: Double-check canister status with `dfx canister status`.
- **Frontend errors**: Confirm all dependencies are installed; run `npm install`.

## License

[MIT License](LICENSE)

## Acknowledgments

- [ICP Ninja](https://icp.ninja) for deployment/hosting.
- [Ollama](https://ollama.com) for the local LLM service.
- [DFINITY](https://dfinity.org/) for the Internet Computer infrastructure.
