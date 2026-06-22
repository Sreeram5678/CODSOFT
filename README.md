# CODSOFT AI & Web Development Project Portfolio

Welcome to the **CODSOFT** project portfolio repository. This workspace consolidates three distinct artificial intelligence and web development applications, organized as git submodules. Each project exhibits modern interface design, complete unit testing suites, and robust algorithmic implementations.

---

## 📂 Repository Structure & Project Map

This workspace uses git submodules to maintain separation of concerns while providing a unified entry point.

```
CODSOFT/ (Root)
├── .gitignore
├── .gitmodules
├── README.md                      # Comprehensive Root Documentation
│
├── chatbot-with-rule-based-responses/ (Submodule 1)
│   ├── intents.json               # Regex Patterns, Intents, and Slots Configuration
│   ├── chatbot.py                 # Core Stateful Rule-Based NLP Classifier CLI
│   ├── server.py                  # Static HTTP Development Server
│   ├── index.html                 # Elegant Responsive Chat UI
│   ├── index.css                  # Modern Glassmorphic Chat Styles
│   ├── app.js                     # Frontend Chatbot logic (JS Mirror of Python classifier)
│   └── test_chatbot.py            # Unit Tests for Chatbot Engine
│
├── tic-tac-toe-ai/ (Submodule 2)
│   ├── backend/
│   │   ├── main.py                # FastAPI Application exposing REST API
│   │   └── minimax.py             # Minimax Solver with Alpha-Beta Pruning & Transposition Cache
│   ├── frontend/
│   │   ├── index.html             # Unbeatable Game Grid UI
│   │   ├── style.css              # Dark/Neon Theme & Interactive Grid Animations
│   │   └── app.js                 # Game state flow & backend API fetch
│   ├── verify_unbeatable.py       # Exhaustive Game Tree Search Simulator
│   ├── test_minimax.py            # Minimax AI solver unit tests
│   └── requirements.txt           # Backend Dependencies (FastAPI, pytest, uvicorn)
│
└── recommendation-system/ (Submodule 3)
    ├── backend/
    │   ├── main.py                # FastAPI endpoints for user history & recommendations
    │   ├── recommender.py         # Hybrid FunkSVD & Cosine Similarity Engine
    │   └── database.py            # SQLite database schema, seeding, and ratings update
    ├── frontend/
    │   ├── index.html             # CineMatch User Dashboard (Tailwind CSS)
    │   └── app.js                 # Dynamic movie list renderer & hybrid blender controller
    ├── tests/
    │   └── test_recommender.py    # Unit tests for SVD training and content filters
    └── Dockerfile                 # Docker configuration for production deployment
```

---

## 🚀 Getting Started

To clone this repository along with all its submodules, run:

```bash
git clone --recursive https://github.com/Sreeram5678/CODSOFT.git
cd CODSOFT
```

If you have already cloned the repository without the submodules, initialize and update them by running:

```bash
git submodule update --init --recursive
```

---

## ☄️ Project 1: Chatbot with Rule-Based Responses

> [!NOTE]
> For detailed documentation, system architecture, and configurations, see the [Chatbot Submodule README.md](file:///Users/sreeramlagisetty/Desktop/CODSOFT/chatbot-with-rule-based-responses/README.md).

A modular, stateful, rules-based chatbot engine featuring natural language processing, slot-filling, and session context tracking. The application is mirrored in both Python (for terminal usage) and JavaScript (for client-side browser execution).

### ⚙️ Core Architecture & NLP Flow
1. **Input Normalizer**: Sanitizes user strings by converting to lowercase (case-folding), stripping punctuation, and collapsing multiple spaces.
2. **Intent Classifier & Slot Filler**: Uses regular expressions with capture groups defined in `intents.json`. If a user mentions their name (e.g., *"my name is Sarah"*), the capture group extracts `Sarah` and updates the context.
3. **Session Manager**: Manages context dictionary variables mapped to distinct user session IDs, enabling context-aware overrides (e.g., welcoming a user back by name).
4. **Response Generator**: Pulls a response template from the matching intent configuration, interpolating active slot values, and choosing random alternatives to prevent repetition.

### 💻 Running the Chatbot
#### Terminal Version (Python)
Run the interactive Python command-line interface:
```bash
cd chatbot-with-rule-based-responses
python chatbot.py
```
*Try typing:* `hello` $\rightarrow$ `my name is Sarah` $\rightarrow$ `hello` (watch it recognize your name).

#### Web Application Version (HTML/JS)
Start the local HTTP web server:
```bash
python server.py
```
Open your browser and navigate to `http://localhost:8080` to experience the modern glassmorphic chat interface.

---

## ❌ Project 2: Unbeatable Tic-Tac-Toe AI

> [!NOTE]
> For detailed documentation, mathematical proofs, system architecture, and local deployment instructions, see the [Tic-Tac-Toe AI Submodule README.md](file:///Users/sreeramlagisetty/Desktop/CODSOFT/tic-tac-toe-ai/README.md).

A web-based Tic-Tac-Toe application powered by an unbeatable Minimax agent. Optimizations like Alpha-Beta Pruning and Transposition Table caching allow the backend to respond in sub-millisecond times ($O(1)$ lookup for repeating states).

### 🧠 Game Theory & Mathematical Optimizations
- **The Minimax Decision Search**: Builds the complete game tree where the AI maximizes utility and the Human minimizes it. Terminal utilities are depth-discounted:
  - AI Win: $+10 - d$ (prefers immediate wins)
  - Human Win: $-10 + d$ (postpones losses)
  - Draw: $0$

$$V(s) = \begin{cases} 
\text{Utility}(s) & \text{if } s \text{ is a terminal state} \\
\max_{a \in \text{Actions}(s)} V(\text{Result}(s, a)) & \text{if Player}(s) = \text{AI (Maximizer)} \\
\min_{a \in \text{Actions}(s)} V(\text{Result}(s, a)) & \text{if Player}(s) = \text{Human (Minimizer)}
\end{cases}$$

- **Alpha-Beta Pruning**: Prunes search branches once the algorithm discovers a move that guarantees a worse outcome than previously assessed choices. Pruning occurs when:

$$\beta \le \alpha$$

- **Fail-Soft Transposition Caching**: Boards with different permutations that result in identical layouts are stored in a transposition cache. To make these cached values depth-neutral, they are normalized before storing and un-normalized when read.

### 💻 Running the Game
1. Create a virtual environment and install dependencies:
   ```bash
   cd tic-tac-toe-ai
   python3 -m venv .venv
   source .venv/bin/activate
   pip install -r requirements.txt
   ```
2. Start the FastAPI backend dev server:
   ```bash
   uvicorn backend.main:app --port 8080
   ```
3. Navigate to `http://127.0.0.1:8080/` in your browser. FastAPI automatically serves the frontend at the root index.

#### 🧪 Running Verification and Tests
- Run solver unit tests:
  ```bash
  python -m unittest test_minimax.py
  ```
- Run API integration tests:
  ```bash
  pytest backend/tests/test_api.py
  ```
- Run the complete game tree simulation (verifies unbeatability across all 255,168 possible board paths):
  ```bash
  python verify_unbeatable.py
  ```

---

## 🎬 Project 3: CineMatch Movie Recommendation System

> [!NOTE]
> For detailed documentation, algorithm explanations, database schema, and REST API specification, see the [CineMatch Submodule README.md](file:///Users/sreeramlagisetty/Desktop/CODSOFT/recommendation-system/README.md).

CineMatch is a movie recommendation engine combining Collaborative Filtering (FunkSVD matrix factorization) and Content-Based Filtering (multi-hot genre vector matching via Cosine Similarity).

### 📊 Algorithmic Design & Mathematics
1. **Collaborative Filtering (FunkSVD)**: Factors the user-movie rating matrix into lower-rank matrices $P$ (user-latent) and $Q$ (movie-latent). Predicted rating $\hat{R}_{u, i}$ is:

$$\hat{R}_{u, i} = \mu + b_u + b_i + P_u \cdot Q_i^T$$

The parameters are updated using Stochastic Gradient Descent (SGD) with $L_2$ regularization:
- $b_u \leftarrow b_u + \gamma (e_{u, i} - \lambda b_u)$
- $b_i \leftarrow b_i + \gamma (e_{u, i} - \lambda b_i)$
- $P_u \leftarrow P_u + \gamma (e_{u, i} Q_i - \lambda P_u)$
- $Q_i \leftarrow Q_i + \gamma (e_{u, i} P_u - \lambda Q_i)$

Where $e_{u,i} = R_{u,i} - \hat{R}_{u,i}$, $\gamma$ is the learning rate, and $\lambda$ is the regularization coefficient.

2. **Content-Based Filtering**: Builds a user genre profile vector $\vec{U}_u$ based on their past ratings (ratings are centered around a baseline of $2.5$):

$$\vec{U}_u = \sum_{i \in H_u} (R_{u, i} - 2.5) \vec{I}_i$$

The content score is the cosine similarity between the user profile and candidate movie genre vector:

$$\text{Score}_{\text{content}}(u, c) = \frac{\vec{U}_u \cdot \vec{I}_c}{\|\vec{U}_u\|_2 \|\vec{I}_c\|_2}$$

3. **Hybrid Blending**: Maps the SVD score to a $[0, 1]$ range and computes the blended recommendation score with blending ratio $\alpha = 0.6$:

$$\text{Score}_{\text{hybrid}}(u, c) = \alpha \cdot \text{Score}_{\text{SVD\_norm}}(u, c) + (1 - \alpha) \cdot \text{Score}_{\text{content}}(u, c)$$

### 💻 Running CineMatch
1. Create a virtual environment and install dependencies:
   ```bash
   cd recommendation-system
   python3 -m venv .venv
   source .venv/bin/activate
   pip install -r backend/requirements.txt
   ```
2. Initialize and seed the SQLite database:
   ```bash
   python backend/database.py
   ```
3. Launch the FastAPI server:
   ```bash
   uvicorn backend.main:app --reload --host 127.0.0.1 --port 8000
   ```
4. Navigate to `http://127.0.0.1:8000/` in your browser. Live ratings dynamically retrain the FunkSVD recommendation model on the fly!
