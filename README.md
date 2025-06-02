# NSFW Detection System

A comprehensive content monitoring system that detects and automatically closes applications displaying explicit content through advanced image analysis and website URL checking.

## 🚨 Important Disclaimer

This software is designed for parental control and workplace monitoring purposes. Use responsibly and in compliance with local laws and regulations. Users are responsible for ensuring proper authorization before monitoring systems or networks they do not own.

## 🔥 Features

### Dual Detection Methods
- **Website URL Checking**: Instantly detects and blocks known NSFW websites
- **Advanced Image Analysis**: Uses computer vision to analyze screen content for explicit material
- **Smart Browser Integration**: Monitors popular browsers (Chrome, Firefox, Edge, Opera, etc.)
- **YouTube Exception**: Excludes YouTube content from detection to prevent false positives

### Aggressive Detection Capabilities
- **Multi-Color Space Analysis**: HSV, YCrCb, and RGB color space skin detection
- **Flesh Concentration Detection**: Identifies high concentrations of flesh-colored pixels
- **Explicit Region Detection**: Analyzes connected components and contour shapes
- **Brightness/Contrast Analysis**: Considers lighting characteristics typical of explicit content

### Real-Time Monitoring
- **Background Operation**: Runs continuously without user interaction
- **Fast Response**: 0.5-second check intervals by default
- **Immediate Termination**: Instantly closes detected applications
- **Process Protection**: Excludes system processes from monitoring

## 📋 Requirements

### Python Packages
```bash
pip install opencv-python psutil pillow numpy pywin32 requests
```

### System Requirements
- **Operating System**: Windows (uses Windows-specific APIs)
- **Python**: 3.6 or higher
- **RAM**: Minimum 2GB available (image processing intensive)
- **Permissions**: Administrator privileges recommended for process termination

## 🚀 Installation

1. **Clone or download** the repository
2. **Install dependencies**:
   ```bash
   pip install opencv-python psutil pillow numpy pywin32 requests
   ```
3. **Run the script**:
   ```bash
   python main.py
   ```

## ⚙️ Configuration

### Sensitivity Levels
- **Low**: `total_score: 35, skin_threshold: 25, explicit_threshold: 20`
- **Medium**: `total_score: 25, skin_threshold: 18, explicit_threshold: 15` (Default)
- **High**: `total_score: 15, skin_threshold: 12, explicit_threshold: 10`

### Monitored Browsers
- Google Chrome (`chrome.exe`)
- Mozilla Firefox (`firefox.exe`)
- Microsoft Edge (`msedge.exe`)
- Opera (`opera.exe`)
- Brave Browser (`brave.exe`)
- Internet Explorer (`iexplore.exe`)
- Safari (`safari.exe`)
- Vivaldi (`vivaldi.exe`)

### Protected Processes
System processes are automatically excluded from monitoring:
- `dwm.exe`, `explorer.exe`, `winlogon.exe`
- `csrss.exe`, `smss.exe`, `wininit.exe`
- `services.exe`, `lsass.exe`, `svchost.exe`
- Development tools: `python.exe`, `cmd.exe`, `powershell.exe`

## 🎯 How It Works

### Detection Pipeline
1. **Active Window Detection**: Identifies the currently focused application
2. **Browser URL Extraction**: For browsers, extracts URLs from window titles
3. **Website Blacklist Check**: Compares URLs against known NSFW domains
4. **Image Analysis**: If no website match, captures and analyzes screen content
5. **Threat Assessment**: Calculates composite scores from multiple detection methods
6. **Action Execution**: Terminates applications exceeding threshold scores

### Image Analysis Techniques
- **Skin Detection**: Multi-range HSV, YCrCb, and RGB color space analysis
- **Morphological Operations**: Noise reduction and region enhancement
- **Connected Components**: Large skin region identification
- **Contour Analysis**: Curved shape detection for body parts
- **Statistical Analysis**: Brightness and contrast evaluation

## 🌐 Website Detection

### Blocked Domains
The system maintains a comprehensive database of NSFW websites including:
- Adult video sites (Pornhub, XVideos, etc.)
- Webcam platforms (Chaturbate, Cam4, etc.)
- Subscription services (OnlyFans, Fansly, etc.)
- Social media with adult content indicators

### Pattern Matching
Advanced regex patterns detect NSFW content indicators:
- URL keywords: `porn`, `xxx`, `sex`, `nude`, `adult`
- Social media NSFW tags: `#nsfw`, `#porn`, `/r/gonewild`
- Adult service patterns: `escort`, `hookup`, `dating.*adult`

## 🔧 Usage

### Automatic Mode (Default)
```bash
python main.py
```
The system starts automatically with medium sensitivity and 0.5-second intervals.

### Manual Configuration
Modify the `AggressiveNSFWDetector` initialization in `main()`:
```python
monitor = AggressiveNSFWDetector(
    check_interval=0.3,    # Faster checking
    sensitivity='high'     # More aggressive detection
)
```

## 📊 Output Information

### Detection Alerts
```
🌐 NSFW WEBSITE DETECTED!
🔗 URL/Title: example-adult-site.com
📋 Reason: Blocked domain: adult-site.com

🚨 EXPLICIT CONTENT DETECTED!
📊 Scores - Total: 28.5, Skin: 22.1, Explicit: 15.3, Flesh: 18.7
🎯 Threshold: 25.0

🚫 DETECTION #1: NSFW Website: Blocked domain: adult-site.com
🚫 CLOSING: chrome.exe - Explicit Website Title
✅ Application terminated successfully
```

### Monitoring Status
```
🔥 AGGRESSIVE NSFW MONITOR ACTIVE
⚙️  Sensitivity: MEDIUM
🔄 Check every: 0.5s
🎯 Will close ANY app showing explicit content
🌐 Now includes website URL checking!
📺 YouTube content is EXCLUDED from detection
🔄 Running continuously in background...
```

## 🛡️ Safety Features

### False Positive Prevention
- **YouTube Exception**: Automatically excludes YouTube content
- **System Process Protection**: Never terminates critical system processes
- **Cooldown Periods**: Prevents rapid successive detections
- **Multi-Factor Validation**: Requires multiple indicators for detection

### Performance Optimization
- **Fast Screenshot Capture**: Optimized screen grabbing
- **Image Resizing**: Reduces processing load while maintaining accuracy
- **Efficient Color Space Conversion**: Minimizes computational overhead
- **Memory Management**: Automatic cleanup of processed images

## ⚠️ Limitations

- **Windows Only**: Uses Windows-specific APIs (win32gui, win32process)
- **English Language**: Optimized for English website patterns
- **Browser Compatibility**: URL extraction may vary between browsers
- **Resource Intensive**: Continuous image processing requires CPU resources
- **Network Content**: Cannot analyze content loaded via AJAX/JavaScript

## 🔧 Troubleshooting

### Common Issues

**Import Errors**
```bash
pip install --upgrade opencv-python psutil pillow numpy pywin32 requests
```

**Permission Denied**
- Run as Administrator
- Check antivirus software interference
- Verify process termination permissions

**High CPU Usage**
- Increase `check_interval` (default: 0.5s)
- Lower sensitivity level
- Close unnecessary applications

**False Positives**
- Add exclusions to `excluded_processes`
- Adjust sensitivity thresholds
- Modify detection patterns

## 📝 Legal Considerations

- Ensure proper authorization before monitoring
- Comply with local privacy laws
- Consider workplace monitoring regulations
- Respect user privacy and consent requirements
- Use only for legitimate parental control or security purposes

## 🔄 Development

### Code Structure
- `AggressiveNSFWDetector`: Main detection class
- `monitor_for_explicit_content()`: Primary monitoring loop
- `aggressive_skin_detection()`: Computer vision analysis
- `is_nsfw_website()`: URL pattern matching
- `close_application()`: Process termination

### Extending Functionality
- Add new NSFW domains to `nsfw_domains` set
- Modify detection patterns in `nsfw_patterns`
- Adjust color space thresholds for different skin tones
- Implement additional browser support

## 📞 Support

For technical issues:
1. Check Python and package versions
2. Verify Windows compatibility
3. Review system permissions
4. Test with different sensitivity levels

---

**Version**: 1.0  
**Compatibility**: Windows 7/8/10/11  
**Python**: 3.6+  
**License**: Use responsibly and legally
