PRIVATE RECORDER 2.0.0

A local-only Chromium extension for recording media from an explicitly enabled HTTPS tab.
It never uploads recordings, has no host_permissions, and does not load remote code.

FEATURES
- Trusted-site gate: YouTube, YouTube Music, Prime Video, Netflix, Spotify and JioHotstar/Hotstar are included.
- Each site can be individually enabled/disabled in Settings.
- Custom HTTPS hostnames are supported, including narrow wildcards like *.example.com.
- Capture modes: Entire tab, Player only, or a user-drawn Custom area.
- Quality modes: Standard (up to 1080p/30), High (up to 1440p/60), Maximum (up to 4K/60).
- Formats: MP4, WebM, M4A and WAV, subject to browser codec support.
- Maximum recording duration: 30, 60, 120, 180 or 240 minutes.
- Automatic stop when media ends; YouTube ad state is handled only on YouTube/YouTube Music.
- Responsive popup and settings UI for narrow and wide screens.
- Download filenames are sanitized and cannot escape the Downloads directory.

INSTALL
1. Unzip the folder somewhere permanent.
2. Open chrome://extensions or edge://extensions.
3. Enable Developer mode.
4. Choose Load unpacked and select this private-recorder folder.
5. Pin Private Recorder to the toolbar.

SECURITY MODEL
- No host_permissions and no tabs permission.
- Only the active tab receiving the user action gets temporary access through activeTab.
- Start is rejected unless the current URL is HTTPS and its hostname exactly matches an enabled site entry (or a permitted subdomain wildcard).
- A recording is bound to the original hostname and stops if the tab navigates away.
- Internal background/offscreen commands use a cryptographically random per-recording token.
- The background worker validates sender context, recording state, target tab, token, file extension, MIME type and blob URL prefix before downloading.
- Strict extension-page CSP blocks remote scripts and normal network connections. connect-src 'self' is used only for same-extension resources.
- No eval(), Function(), inline scripts, network APIs, analytics, accounts or tracking.
- Download names are generated from sanitized text and a timestamp and are always relative to the Downloads directory.
- Maximum duration is enforced with chrome.alarms so a service-worker suspension cannot silently remove the safety limit.

IMPORTANT
This records what the browser exposes through tabCapture. It does not bypass DRM or browser security controls.
Use only content you are authorized to record. Whether recording or keeping a particular work is lawful depends on the content and your permissions.

CODE AUDIT
Run: node tests/shared.test.mjs
Then check the extension in chrome://extensions with the unpacked folder. The CHECKSUMS.txt file lets you verify the final build files.
