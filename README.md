# AI-Based Dynamic Scenario Simulation Game 🎮🤖

An intelligent, choice-driven interactive game built with Flutter where AI generates unique scenarios in real-time. Each playthrough is a 3-4 round adventure with dynamic storytelling powered by **Groq AI**.

---

## 🌟 Features

- **AI-Powered Scenarios** - Real-time scenario generation using Groq LLaMA 3.1
- **Dynamic Choices** - AI-generated branching dialogue options based on your decisions
- **Anonymous Auth** - Firebase Authentication for seamless user experience
- **Game History** - Firestore integration to save and track completed runs
- **Multi-Platform** - Runs on Android, iOS, Web, and Desktop (Flutter)
- **Theme & Tone Customization** - Generate scenarios with different themes and tones
- **Flexible Deployment** - Firebase Functions or Render backend options
- **Health Monitoring** - Built-in API health checks

---

## 🎯 How It Works

1. **Start Game** - Select a theme and tone for your scenario
2. **AI Generation** - Backend generates initial scenario with 3-4 choices using Groq AI
3. **Make Decisions** - Choose your action and watch the story evolve
4. **Continue** - AI adapts the next scenario based on your choice
5. **Complete & Save** - Game session is saved to Firestore history

---

## 💻 Tech Stack

### Frontend
- **Framework**: Flutter (Dart)
- **Authentication**: Firebase Auth (Anonymous)
- **Database**: Cloud Firestore
- **HTTP Client**: Dart http package

### Backend
- **Primary**: Node.js + Express
- **Alternative**: Firebase Cloud Functions
- **AI Provider**: Groq (LLaMA 3.1 8B Instant)
- **Deployment**: Firebase Hosting or Render

### Infrastructure
- **Firebase**: Auth, Firestore, Functions, Hosting
- **Render**: Alternative serverless deployment
- **Version Control**: GitHub

---

## 📁 Project Structure

```
flutter-ai-game/
├── lib/                    # Flutter app source code
├── backend/                # Local Node.js development server
│   └── src/
│       ├── index.js       # Main server
│       ├── game-service.js # Game logic
│       └── providers.js   # AI provider abstraction
├── functions/             # Firebase Cloud Functions
├── firebase/              # Firebase configuration files
├── android/               # Android-specific code
├── ios/                   # iOS-specific code
├── web/                   # Web build target
├── branding/              # App branding assets
├── pubspec.yaml          # Flutter dependencies
├── firebase.json         # Firebase config
├── render.yaml           # Render deployment config
└── firestore.rules       # Firestore security rules
```

---

## 🚀 Getting Started

### Prerequisites

- **Flutter SDK** (v3.10.7+)
- **Node.js** (v14+)
- **Firebase Account** (for backend & storage)
- **Groq API Key** (for AI generation)

### 1. Backend Setup

```bash
cd backend
cp .env.example .env
# Edit .env and add your Groq API key
node src/index.js
```

Health check:
```bash
curl http://localhost:8787/health
```

### 2. Frontend Setup

Create Firebase config:
```bash
cp firebase/flutter_config.example.json firebase/flutter_config.local.json
# Fill in your Firebase credentials
```

Run the app:
```bash
# Android emulator
flutter run --dart-define-from-file=firebase/flutter_config.local.json

# Physical device
flutter run --dart-define-from-file=firebase/flutter_config.local.json
```

---

## 🔧 Configuration

### Backend Environment (`.env`)

```env
HOST=localhost
PORT=8787
USE_MOCK_AI=false
AI_API_URL=https://api.groq.com/openai/v1/chat/completions
AI_API_KEY=your_groq_api_key_here
AI_MODEL=llama-3.1-8b-instant
DEFAULT_MAX_ROUNDS=4
```

### Flutter Firebase Config

For Android emulator:
```json
{
  "API_BASE_URL": "http://10.0.2.2:8787",
  "FIREBASE_API_KEY": "your_key",
  "FIREBASE_PROJECT_ID": "your_project"
}
```

For iOS simulator/desktop:
```json
{
  "API_BASE_URL": "http://localhost:8787",
  "FIREBASE_API_KEY": "your_key",
  "FIREBASE_PROJECT_ID": "your_project"
}
```

---

## 📡 API Endpoints

### POST `/game/start`
Generate a new game scenario.

**Request:**
```json
{
  "theme": "relationship_chaos",
  "tone": "dark_comedy",
  "maxRounds": 4,
  "promptHint": "boyfriend and girlfriend drama with social-media chaos"
}
```

**Response:**
```json
{
  "sessionId": "uuid",
  "scenario": "...",
  "choices": [
    { "id": "a", "text": "Option A" },
    { "id": "b", "text": "Option B" },
    { "id": "c", "text": "Option C" }
  ],
  "round": 1,
  "maxRounds": 4
}
```

### POST `/game/continue`
Continue game with user's choice.

**Request:**
```json
{
  "sessionId": "session-id",
  "selectedChoiceId": "a",
  "selectedChoiceText": "Reply with interesting response"
}
```

### GET `/health`
Health check endpoint.

---

## 🌐 Deployment

### Option 1: Firebase Functions + Hosting

```bash
# 1. Configure Firebase
firebase login
cp .firebaserc.example .firebaserc
# Edit .firebaserc with your project ID

# 2. Deploy
firebase deploy --only functions,firestore:rules,hosting
```

### Option 2: Render (Node Backend)

1. Push repo to GitHub
2. Create Web Service on Render
3. Set root directory to `backend`
4. Add environment variable: `AI_API_KEY=your_key`
5. Update Flutter `API_BASE_URL` to Render URL

---

## 📊 Game Themes

Pre-defined themes for scenario generation:
- `relationship_chaos` - Romantic drama
- `workplace_drama` - Office conflicts
- `adventure_quest` - Fantasy scenarios
- `sci_fi_crisis` - Futuristic challenges
- `mystery_puzzle` - Detective storylines

Customize themes in `backend/src/game-service.js`

---

## 🧪 Testing

### Flutter
```bash
flutter analyze
flutter test
```

### Backend
```bash
cd backend
node --test
```

### Firebase Functions
```bash
node --check functions/index.js
node --check functions/src/game-service.js
```

---

## 📊 Database Schema (Firestore)

```
users/{uid}/
└── game_history/{sessionId}
    ├── theme: string
    ├── tone: string
    ├── startedAt: timestamp
    ├── completedAt: timestamp
    ├── rounds: number
    ├── choices: array
    └── finalOutcome: string
```

---

## 🔐 Security

- **Firebase Firestore Rules** - User-specific access control
- **Anonymous Auth** - No personal data required
- **API Validation** - Input sanitization on backend
- **Environment Variables** - Sensitive keys in `.env`

---

## 🤝 Contributing

Contributions welcome! Areas for improvement:
- Add new game themes
- Enhance AI prompt engineering
- Improve UI/UX
- Add multiplayer support
- Performance optimization

---

## 📝 License

Open source under MIT License.

---

## 👤 Author

**Amit Shakya**
- GitHub: [@0-Amit-0](https://github.com/0-Amit-0)
- Portfolio: [0-Amit-0.github.io](https://0-Amit-0.github.io)

---

## 🐛 Troubleshooting

### Backend not connecting
- Check `API_BASE_URL` matches your setup
- Verify `backend` process is running
- Try `curl http://localhost:8787/health`

### Firebase errors
- Ensure Firestore database exists
- Check Firebase Rules are deployed
- Verify credentials in `flutter_config.local.json`

### AI not generating
- Verify Groq API key is valid
- Check API rate limits
- Test with `USE_MOCK_AI=true` first

---

**Star this project if you enjoyed it! ⭐**
