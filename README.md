# CropWise: Advanced Plant Analysis Tool

**CropWise** is an AI-powered plant analysis tool designed specifically for South African farmers. It leverages Google's Generative AI (Gemini) to analyze plant images, identify species, assess health, and provide localized care recommendations and treatment options suited to South African agriculture.

## Features

- 🌱 **Species Identification**: Accurately identify plant species from images
- 💚 **Health Assessment**: Detailed plant health analysis and disease detection
- 📋 **Care Recommendations**: Customized care and treatment advice specific to South African farming conditions
- ⚡ **Fast Processing**: Instant AI-powered analysis results
- 📄 **PDF Reports**: Generate and download detailed plant analysis reports
- 🖱️ **Drag & Drop Upload**: Intuitive image upload with preview
- 🔐 **User Authentication**: Secure sign-up and sign-in with Firebase

## Tech Stack

**Backend:**
- Node.js + Express.js
- Google Generative AI (Gemini 1.5 Flash)
- Multer (file upload handling)
- PDFKit (PDF generation)
- Firebase (authentication)
- Dotenv (environment configuration)

**Frontend:**
- HTML5, CSS3, JavaScript (ES6+)
- Firebase Authentication (client-side)
- Font Awesome (icons)

**Database & Storage:**
- Firebase Authentication

## Prerequisites

- Node.js (v14 or higher)
- npm or yarn
- Google API credentials (Gemini API key)
- Firebase project configured

## Installation

1. **Clone or extract the project**
   ```bash
   cd CropWise1
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   - Create a `.env` file in the root directory
   - Add your credentials:
     ```
     GEMINI_API_KEY=your_google_generative_ai_key_here
     PORT=5000
     ```

4. **Start the server**
   ```bash
   npm start
   ```
   For development with auto-reload:
   ```bash
   npm run dev
   ```

5. **Access the application**
   - Open your browser and navigate to `http://localhost:5000`

## How to Use

### For Farmers/Users

1. **Sign Up/Sign In**
   - Click "Sign Up" on the landing page to create an account
   - Enter your email and password
   - Or click "Sign In" if you already have an account

2. **Analyze a Plant**
   - Navigate to the Analysis page (auto-redirected after login)
   - Upload a plant image by:
     - Clicking the upload area and selecting a file, OR
     - Dragging and dropping an image directly
   - Click "Analyze Plant" button
   - Wait for AI analysis to complete

3. **View Results**
   - Your analysis results appear showing:
     - Plant species identification
     - Health status
     - Disease/pest detection (if any)
     - Localized care recommendations
     - Treatment options for South African conditions

4. **Download Report**
   - Click "Download PDF Report" to get a detailed PDF with analysis and plant image

## Project Structure

```
CropWise1/
├── app.js                    # Express server & API routes
├── package.json              # Dependencies & scripts
├── .env                      # Environment variables (create this)
├── public/                   # Frontend assets served statically
│   ├── index.html           # Landing/auth page
│   ├── analyze.html         # Plant analysis page
│   ├── css/
│   │   ├── landing.css      # Landing page styles
│   │   └── styles.css       # Analysis page styles
│   └── js/
│       ├── firebaseConfig.js # Firebase setup
│       ├── auth.js          # Authentication functions
│       ├── landing.js       # Landing page logic & dialogs
│       ├── main.js          # Analysis page logic
│       ├── apiService.js    # API communication wrapper
│       └── imageHandler.js  # Image upload & preview handling
└── reports/                 # Generated PDF reports (auto-created)
```

## API Routes

### POST `/analyze`
Analyzes a plant image using Gemini AI.

**Request:**
- Multipart form data with image file

**Response:**
```json
{
  "result": "Plant analysis text...",
  "image": "data:image/jpeg;base64,..."
}
```

### POST `/download`
Generates and downloads a PDF report.

**Request:**
```json
{
  "result": "Analysis text",
  "image": "base64 image data"
}
```

**Response:** PDF file stream

## Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `GEMINI_API_KEY` | Google Generative AI API key | Yes |
| `PORT` | Server port (default: 5000) | No |

## Important Notes

- **Credentials**: Never commit `.env` file with real API keys to version control
- **Authentication**: Currently auth users are redirected to analyze page, but routes are not protected server-side. Consider adding auth middleware if deploying to production
- **Image Upload**: Images are temporarily stored in `upload/` directory and automatically deleted after analysis
- **PDF Reports**: Generated PDFs are stored in `reports/` directory; consider implementing cleanup or cloud storage for production use

## Development

### Available Scripts

```bash
npm start     # Start server
npm run dev   # Start server with auto-reload (nodemon)
npm test      # Run tests (not yet configured)
```

### Code Quality

- JavaScript (ES6+ on frontend, CommonJS on backend)
- CSS organized by page (landing.css, styles.css)
- Modular JavaScript with class-based handlers

## Known Limitations & Future Improvements

- No server-side auth middleware (all routes are publicly accessible)
- No input validation on image MIME types beyond client-side
- Single image analysis (no batch processing)
- No user dashboard or analysis history
- PDF reports auto-deleted after download (no persistent storage)
- No multi-language support implementation (feature listed but not active)

### Recommended Improvements for Production

1. Add authentication middleware to `/analyze` and `/download` routes
2. Implement strict image validation (MIME type, file size limits)
3. Add error handling for Gemini API rate limits and failures
4. Store generated reports in cloud storage (Firebase Storage, AWS S3)
5. Implement analysis history for logged-in users
6. Add logging and monitoring
7. Implement input sanitization to prevent XSS

## Troubleshooting

**Issue: "GEMINI_API_KEY not found"**
- Ensure `.env` file exists in root directory with valid Gemini API key

**Issue: "Cannot find module 'express'"**
- Run `npm install` to install all dependencies

**Issue: "Port 5000 already in use"**
- Change PORT in `.env` or kill the existing process on port 5000

**Issue: Images fail to upload**
- Check browser console for errors
- Ensure image file size is reasonable (under 50MB)
- Verify network connection

## License

ISC

## Support

For issues or questions, please refer to the code comments or documentation in individual files.

---

**Created:** April 2026  
**Version:** 1.0.0
