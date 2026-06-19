# Contributing to My Sweet Home

Thank you for your interest in contributing to My Sweet Home! We welcome all contributions and appreciate your help in making this project better.

## 📋 Table of Contents
- [Getting Started](#getting-started)
- [Code of Conduct](#code-of-conduct)
- [How to Contribute](#how-to-contribute)
- [Development Setup](#development-setup)
- [Submitting Changes](#submitting-changes)
- [Style Guidelines](#style-guidelines)
- [Questions?](#questions)

## Getting Started

1. **Fork the repository** on GitHub
2. **Clone your fork** locally
3. **Create a new branch** for your feature or fix
4. **Make your changes** following our guidelines
5. **Submit a pull request** with a clear description

## Code of Conduct

Please note that this project is released with a [Contributor Code of Conduct](CODE_OF_CONDUCT.md). By participating in this project you agree to abide by its terms.

## How to Contribute

### Reporting Bugs
- Check if the bug is already reported in [Issues](https://github.com/seeethome321/my-sweet-home/issues)
- If not, create a new issue with:
  - Clear, descriptive title
  - Detailed description of the bug
  - Steps to reproduce
  - Expected vs. actual behavior
  - Screenshots/videos if applicable
  - Your browser/system information

### Suggesting Enhancements
- Check existing [Issues](https://github.com/seeethome321/my-sweet-home/issues) for similar suggestions
- Create a new issue with:
  - Clear, descriptive title
  - Detailed description of the enhancement
  - Why this enhancement would be useful
  - Possible implementation approach

### Contributing Code
- Look for issues labeled `good first issue` or `help wanted`
- Comment on an issue to express interest
- Fork and create a feature branch
- Follow the style guidelines (see below)
- Make your changes and test thoroughly
- Submit a pull request

## Development Setup

1. **Fork and clone**
   ```bash
   git clone https://github.com/YOUR-USERNAME/my-sweet-home.git
   cd my-sweet-home
   ```

2. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Make your changes**
   - Keep commits focused and logical
   - Write clear commit messages
   - Reference issues when applicable

4. **Test your changes**
   - Open the application in multiple browsers
   - Test on different screen sizes
   - Verify new features work correctly

## Submitting Changes

1. **Push to your fork**
   ```bash
   git push origin feature/your-feature-name
   ```

2. **Open a Pull Request** with:
   - Clear title describing the changes
   - Description of what was changed and why
   - Reference to related issues
   - Screenshots for UI changes
   - Confirmation that tests have been run

3. **Respond to feedback** from maintainers
   - Be open to suggestions
   - Make requested changes promptly
   - Re-request review when ready

## Style Guidelines

### JavaScript
```javascript
// Use meaningful variable names
const propertyAddress = "123 Main St";

// Use consistent indentation (2 spaces)
function manageProperty(property) {
  if (property) {
    return property.manage();
  }
}

// Add comments for complex logic
// Calculate rental income for the period
const monthlyIncome = properties.reduce((sum, prop) => {
  return sum + prop.rent;
}, 0);
```

### HTML
```html
<!-- Use semantic HTML -->
<section class="property-management">
  <h2>Properties</h2>
  <article class="property-card">
    <h3>Property Name</h3>
    <p>Description</p>
  </article>
</section>

<!-- Use meaningful class names -->
<button class="btn-primary">Submit</button>
```

### CSS
```css
/* Use BEM naming convention */
.property-card {
  border: 1px solid #ddd;
  padding: 20px;
}

.property-card__title {
  font-size: 18px;
  margin-bottom: 10px;
}

.property-card__button {
  background-color: #007bff;
  color: white;
}
```

## General Guidelines

- Use clear, descriptive names for variables and functions
- Keep functions small and focused on a single task
- Comment complex or non-obvious code
- Use consistent formatting throughout
- Test on modern browsers (Chrome, Firefox, Safari, Edge)
- Ensure responsive design works on mobile/tablet/desktop

## Commit Messages

Write clear commit messages:

```
// Good
Fix bug in property deletion logic
Add validation for tenant email addresses
Update documentation for setup process

// Avoid
Fixed bugs
Updated code
Changes
```

## Pull Request Process

1. Ensure all tests pass
2. Update README.md with any new features
3. Increase version numbers following [Semantic Versioning](https://semver.org/)
4. Describe your changes in the PR
5. Link related issues
6. Be ready to respond to feedback

## Recognition

Contributors will be recognized in:
- [CONTRIBUTORS.md](CONTRIBUTORS.md)
- GitHub contributors page
- Project updates and announcements

## Questions?

- Ask in the [Discussions](https://github.com/seeethome321/my-sweet-home/discussions)
- Open an issue for guidance
- Check existing documentation

---

**Thank you for contributing to My Sweet Home! 🙏**