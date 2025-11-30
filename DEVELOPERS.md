# Developer Guide

This guide provides technical details for developers who want to understand, modify, or extend the Body & Mind Detective application.

## 🏗️ Architecture Overview

Body & Mind Detective is intentionally designed as a **single-file HTML application** with zero dependencies. This architecture decision enables:

- **Zero build process** - Open and run immediately
- **Maximum portability** - Works anywhere HTML works
- **Easy deployment** - Single file upload to any host
- **No package management** - No npm, webpack, or bundlers needed
- **Offline capable** - Can be run from local filesystem

## 📂 Code Structure

The `index.html` file contains three main sections:

### 1. Head Section
```html
<head>
  <!-- Fonts from Google Fonts -->
  <!-- CSS Variables & Styles -->
</head>
```

**Design Tokens (CSS Variables):**
```css
:root {
  --gold-primary: #D4AF37;
  --gold-dark: #C5A000;
  --red-orange: #FF4500;
  --cream-bg: #F9F7F2;
  /* ... more tokens */
}
```

### 2. Body Section (5 Pages)
```html
<body>
  <!-- Landing Page -->
  <div id="landingPage" class="page active">...</div>
  
  <!-- Student Quiz Page -->
  <div id="studentQuizPage" class="page">...</div>
  
  <!-- Student Results Page -->
  <div id="studentResultsPage" class="page">...</div>
  
  <!-- Teacher Quiz Page -->
  <div id="teacherQuizPage" class="page">...</div>
  
  <!-- Teacher Results Page -->
  <div id="teacherResultsPage" class="page">...</div>
</body>
```

### 3. JavaScript Section
```javascript
<script>
  // State Management
  let studentAnswers = {};
  let teacherAnswers = Array(5).fill(null);
  let teacherIntensities = Array(5).fill(5);
  
  // Navigation Functions
  // Quiz Logic Functions
  // Results Processing Functions
</script>
```

## 🎨 Design System

### Typography Scale
- **Display (h1)**: 2-3.5rem (clamp for responsive)
- **Headings (h2, h3)**: 1.5-2.25rem
- **Body**: 16px base (1rem)
- **Small text**: 0.85-0.9rem

### Spacing System
- **Container padding**: 2rem (desktop) / 1.5rem (mobile)
- **Card padding**: 2.5rem (desktop) / 1.5rem (mobile)
- **Component gaps**: 1rem, 1.5rem, 2rem, 3rem

### Animation Timing
- **Page transitions**: 0.4s ease-in-out
- **Hover effects**: 0.3s ease
- **Breathing bubble**: 8s infinite ease-in-out

## 🔧 Key Functions

### Navigation
```javascript
showPage(pageId)          // Show specific page, hide others
goHome()                  // Return to landing page, reset state
```

### Student Quiz
```javascript
selectStudentAnswer(questionNum, answer)  // Record answer, advance question
updateStudentProgress()                   // Update progress bar
showStudentResults()                      // Analyze answers, show personalized results
```

### Teacher Assessment
```javascript
selectTeacherAnswer(questionIndex, answer)  // Toggle Yes/No, show/hide slider
submitTeacherQuiz()                         // Validate completion, show results
showTeacherResults()                        // Calculate risk level, show toolkit
toggleStrategy(card)                        // Expand/collapse strategy cards
```

## 🎯 State Management

The application uses simple JavaScript variables for state (no Redux, Vuex, etc.):

```javascript
// Student state
studentAnswers = {
  1: 'hungry',    // Question 1 answer
  2: 'explode',   // Question 2 answer
  3: 'tight',     // Question 3 answer
  4: 'stormy'     // Question 4 answer
}

// Teacher state
teacherAnswers = ['yes', 'no', 'yes', null, 'yes']  // Yes/No for each question
teacherIntensities = [7, 5, 8, 5, 6]                // Slider values (1-10)
```

**State resets** when user clicks "Home" button or reloads the page.

## 🧪 Testing Checklist

### Browser Compatibility
Test on:
- Chrome (latest 2 versions)
- Firefox (latest 2 versions)
- Safari (latest 2 versions)
- Edge (latest version)
- Mobile Safari (iOS)
- Mobile Chrome (Android)

### Functional Testing

**Student Quiz:**
- [ ] All 4 questions display correctly
- [ ] Emoji buttons are clickable and provide visual feedback
- [ ] Progress bar updates correctly
- [ ] Results page shows appropriate strategy
- [ ] Breathing bubble animates smoothly
- [ ] Home button resets quiz

**Teacher Assessment:**
- [ ] All 5 questions display correctly
- [ ] Yes/No buttons toggle properly
- [ ] Sliders appear/disappear based on Yes/No selection
- [ ] Slider values update correctly
- [ ] Progress bar updates as questions are answered
- [ ] Submit button validates all questions answered
- [ ] Results correctly categorize risk level (Low/Moderate/High)
- [ ] Strategy cards expand/collapse on click
- [ ] External links open in new tabs

**Navigation:**
- [ ] Landing page displays on load
- [ ] Home button appears on all pages except landing
- [ ] Page transitions are smooth (no flash)
- [ ] Back button doesn't break state

**Responsive Design:**
- [ ] Layout works on 320px width (small phones)
- [ ] Layout works on tablets (768px)
- [ ] Layout works on desktop (1024px+)
- [ ] Text is readable at all sizes
- [ ] Touch targets are large enough on mobile (44px minimum)

## 🎨 Making Design Changes

### Changing Colors
Edit CSS variables in the `:root` selector:
```css
:root {
  --gold-primary: #YourNewColor;
  --gold-dark: #YourNewColor;
  /* etc. */
}
```

### Adding New Questions

**For Student Quiz:**
1. Add question HTML in `studentQuizPage`
2. Update progress calculation (change `/4` to new total)
3. Add logic in `selectStudentAnswer()`
4. Update result analysis in `showStudentResults()`

**For Teacher Assessment:**
1. Add question in `teacherQuizPage`
2. Update arrays: `teacherAnswers = Array(6).fill(null)` (change 5 to 6)
3. Add slider listener in DOMContentLoaded
4. Update progress calculation in `selectTeacherAnswer()`

### Modifying Strategies
Edit the HTML inside `showStudentResults()` or the strategy cards in `teacherResultsPage`.

## 🚀 Deployment Options

### Option 1: GitHub Pages (Recommended)
Already configured with GitHub Actions workflow in `.github/workflows/deploy.yml`

1. Push to main branch
2. Workflow automatically deploys
3. Live at: `https://[username].github.io/[repo-name]/`

### Option 2: Netlify
1. Drag and drop `index.html` to Netlify dashboard
2. Or connect GitHub repository
3. No build settings needed

### Option 3: Traditional Web Host
1. Upload `index.html` via FTP
2. Access at: `https://yourdomain.com/index.html`

### Option 4: Cloudflare Pages
1. Connect GitHub repository
2. Build settings: None needed
3. Output directory: `/`

## 🔒 Security Considerations

### No Backend = No Server-Side Vulnerabilities
- No SQL injection risk
- No server-side authentication to breach
- No API keys to expose

### Client-Side Best Practices
- **No eval()** - We don't use eval or Function constructor
- **No innerHTML with user input** - We use textContent where appropriate
- **CSP friendly** - Inline scripts are isolated and minimal
- **No external dependencies** - Reduces supply chain attack surface

### Privacy by Design
- **No data storage** - Nothing sent to servers
- **No cookies** - No tracking
- **No analytics** - Completely private
- **Session only** - Data clears on page reload

## 📈 Performance Optimization

Current performance metrics:
- **File size**: ~20KB (uncompressed HTML)
- **Load time**: < 100ms (local) / < 500ms (CDN)
- **First paint**: < 200ms
- **Interactive**: Immediately

### If You Need to Optimize Further:
1. **Minify CSS** - Remove whitespace, comments
2. **Inline critical fonts** - Convert to base64 (trade-off: larger file)
3. **Compress images** - If you add any
4. **Defer non-critical scripts** - Move some JS to async/defer

## 🌐 Internationalization (i18n)

To add language support:

1. Extract all user-facing strings to a language object:
```javascript
const lang = {
  en: {
    title: "Body & Mind Detective",
    studentBtn: "I am a Student",
    // ... etc
  },
  es: {
    title: "Detective del Cuerpo y la Mente",
    studentBtn: "Soy un Estudiante",
    // ... etc
  }
};
```

2. Add language selector to UI
3. Update all text content dynamically
4. Consider RTL support for Arabic, Hebrew

## 🤝 Code Style Guide

### Naming Conventions
- **Functions**: camelCase - `selectStudentAnswer()`
- **Variables**: camelCase - `studentAnswers`, `teacherIntensities`
- **IDs**: camelCase - `studentQuizPage`, `homeBtn`
- **Classes**: kebab-case - `glass-card`, `emoji-btn`
- **CSS Variables**: kebab-case - `--gold-primary`, `--cream-bg`

### Comments
```javascript
// Single-line for brief explanations
function simple() { /* ... */ }

/**
 * Multi-line for complex functions
 * @param {number} questionNum - Question index (1-4)
 * @param {string} answer - The selected answer
 */
function complex(questionNum, answer) { /* ... */ }
```

## 📚 Extending the Application

### Ideas for Extensions
1. **Data Export** - Add JSON download of results
2. **Print Stylesheet** - Optimize for printing results
3. **PWA** - Add service worker for offline use
4. **Accessibility** - Add ARIA live regions for screen readers
5. **Analytics (Privacy-friendly)** - Use Plausible or Fathom
6. **Multi-quiz** - Allow saving multiple student assessments

### Keeping Single-File Architecture
If you must add complexity while maintaining single-file:
- Use ES6 modules within `<script type="module">`
- Inline SVG icons instead of icon fonts
- Use CSS Grid/Flexbox instead of framework layouts
- Leverage Web APIs (Storage, Notifications) instead of libraries

## 🐛 Debugging Tips

### Common Issues
1. **Page won't show**: Check `showPage()` is called correctly
2. **Styles not applying**: Verify CSS selector specificity
3. **State not resetting**: Ensure `goHome()` resets all variables
4. **Mobile layout broken**: Test with browser DevTools device emulation

### Browser DevTools
- **Chrome DevTools**: F12 → Console for errors, Elements for DOM
- **Firefox Developer Tools**: F12 → similar features
- **Safari Web Inspector**: Cmd+Opt+I on Mac

## 📞 Getting Help

If you're stuck:
1. Check existing [GitHub Issues](https://github.com/mariorazo97/quizmybrainz-wellness-tool/issues)
2. Review this developer guide
3. Open a new issue with `[QUESTION]` tag
4. Visit [QuizMyBrainz.com](https://quizmybrainz.com/contact-us/) for support

---

**Happy coding! 🚀**
