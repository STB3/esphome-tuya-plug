# Contributing to ESPHome Tuya Smart Plug

Thank you for your interest in contributing! This document provides guidelines for contributing to this project.

## How to Contribute

### Reporting Bugs

If you find a bug, please create an issue with:

1. **Clear Title**: Descriptive summary of the issue
2. **Description**: Detailed explanation of the problem
3. **Steps to Reproduce**: Numbered list of steps to recreate the issue
4. **Expected Behavior**: What should happen
5. **Actual Behavior**: What actually happens
6. **Environment Details**:
   - ESPHome version
   - Home Assistant version (if applicable)
   - Hardware revision
   - Any modifications made

**Example**:
```
Title: Power sensor reports incorrect values after OTA update

Description: After performing an OTA update from v1.0 to v1.1, the power 
sensor reports values that are 10x higher than actual consumption.

Steps to Reproduce:
1. Flash device with v1.0
2. Verify power readings are accurate
3. Perform OTA update to v1.1
4. Observe power readings

Expected: Power readings should remain accurate
Actual: Power readings are multiplied by 10

Environment:
- ESPHome 2024.11.0
- Home Assistant 2024.11.3
- Original Tuya hardware, no modifications
```

### Suggesting Enhancements

Enhancement suggestions are welcome! Please create an issue with:

1. **Use Case**: Describe what you're trying to accomplish
2. **Proposed Solution**: Your idea for implementing the feature
3. **Alternatives Considered**: Other approaches you've thought about
4. **Benefits**: Why this would be useful for others

### Submitting Pull Requests

1. **Fork the Repository**
   ```bash
   git clone https://github.com/yourusername/esphome-tuya-plug.git
   cd esphome-tuya-plug
   ```

2. **Create a Branch**
   ```bash
   git checkout -b feature/your-feature-name
   # or
   git checkout -b fix/your-bug-fix
   ```

3. **Make Your Changes**
   - Follow the existing code style
   - Test thoroughly on actual hardware
   - Update documentation if needed
   - Add comments for complex logic

4. **Commit Your Changes**
   ```bash
   git add .
   git commit -m "Add feature: brief description"
   ```
   
   Use clear commit messages:
   - `Add:` for new features
   - `Fix:` for bug fixes
   - `Update:` for changes to existing features
   - `Docs:` for documentation changes

5. **Push and Create Pull Request**
   ```bash
   git push origin feature/your-feature-name
   ```
   
   Then create a pull request on GitHub with:
   - Clear description of changes
   - Link to related issues
   - Test results
   - Screenshots (if UI changes)

## Code Guidelines

### YAML Style

- Use 2 spaces for indentation
- Keep lines under 100 characters
- Add comments for non-obvious configurations
- Group related configurations together
- Use meaningful IDs and names

**Example**:
```yaml
# Power monitoring sensors with descriptive names
sensor:
  - platform: bl0942
    uart_id: bl0942_uart
    voltage:
      name: 'Mains Voltage'
      id: voltage_sensor
    current:
      name: 'Load Current'
      id: current_sensor
```

### Documentation

- Update README.md if adding features
- Include wiring diagrams for hardware changes
- Add troubleshooting tips for common issues
- Provide configuration examples

### Testing

Before submitting, test:

- ✅ Initial flash from stock firmware
- ✅ OTA updates
- ✅ All sensors reporting correctly
- ✅ Relay operation (manual and via HA)
- ✅ WiFi reconnection after router restart
- ✅ Power monitoring accuracy (compare with known loads)
- ✅ Web interface accessibility
- ✅ Long-term stability (24+ hours)

## Hardware Variations

If you have a different hardware revision:

1. Document the differences (GPIO pins, chips, etc.)
2. Provide clear photos of the PCB
3. Test thoroughly before submitting
4. Update the README with hardware variant information
5. Consider creating a separate configuration file

## Safety Considerations

⚠️ All contributions must prioritize safety:

- Never suggest modifications that compromise electrical safety
- Include appropriate warnings for high-voltage work
- Recommend proper insulation and enclosure
- Advise users to follow local electrical codes
- Suggest professional inspection for modifications

## License

By contributing, you agree that your contributions will be licensed under the same Custom Non-Commercial License as the project. See the LICENSE file for details.

If you're making a significant contribution and want commercial use rights for your specific contribution, please discuss this in your pull request.

## Questions?

- Open an issue with the "question" label
- Check existing issues and discussions
- Be patient and respectful

## Recognition

Contributors will be acknowledged in:
- README.md (Contributors section)
- Release notes for significant contributions
- Special thanks for bug reports and testing

Thank you for helping improve this project!
