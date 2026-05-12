# Contributing to Smart Irrigation System

Thank you for your interest in contributing! 🌱

---

## How to Contribute

### Report a Bug
- Open an [Issue](../../issues) with label `bug`
- Include your board (Uno/ESP32), sensor type, and what happened

### Suggest a Feature
- Open an [Issue](../../issues) with label `enhancement`
- Describe the use case and expected behaviour

### Submit a Pull Request

1. Fork the repository
2. Create a feature branch:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. Make your changes
4. Test on actual hardware if possible
5. Commit with a clear message:
   ```bash
   git commit -m "feat: add OLED display support"
   ```
6. Push and open a PR against `main`

---

## Code Style

- Use `const` for pin numbers and thresholds
- Prefer `millis()` over `delay()` for timing
- Add comments for non-obvious logic
- Keep pin definitions at the top of the file
- Use `F()` macro for string literals on Uno to save RAM

---

## Commit Message Format

```
type: short description

Types: feat | fix | docs | refactor | test | chore
```

Examples:
- `feat: add capacitive sensor support`
- `fix: correct ESP32 ADC pin conflict with Wi-Fi`
- `docs: update calibration guide`
