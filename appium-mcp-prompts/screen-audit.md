# Capture Screenshots of the Mobile App:
Using the Appium MCP Server (#mcp-appium), perform a complete screen capture audit of the android mobile application:

Note:
1. Appium Server is already running.
2. The Scriptlab android app is located in the app/android folder.

## Objectives
1. **Application Setup**
 - Identify the target mobile app (name, package ID, platform)
 - Launch the application on the connected emulator
 - Verify app is running and fully initialized

2. **Authentication**
 - Login using following credentials:
   - Username: `scriptlab`
   - Password: `scriptlab123`
 - Confirm successful navigation to Home screen

3. **Automated Screen Discovery**
 - Systematically explore the app's navigation structure
 - Identify all accessible screens, views, and states
 - Map out the navigation hierarchy and flow

4. **Comprehensive Screenshot Capture**

**Core Screens**
 - Splash/Loading screen
 - Login/Authentication screens
 - Main/Home screen
 - All primary navigation destinations (tabs, menu items)

**Secondary Screens**
 - Settings and configuration screens
 - Profile/Account screens
 - Help/Support screens
 - About/Information screens

**Interactive Elements**
 - Modal dialogs and popups
 - Dropdown menus (expanded state)
 - Bottom sheets and drawers (open state)
 - Toast messages or snackbars (if triggerable)

**Data States**
 - Empty states (no data available)
 - Loaded states (with sample data)
 - Error states (if safely replicable)
 - Loading states (if capturable)

**Form Screens**
 - All input forms
 - Validation error states
 - Success confirmation screens

5. **Capture Standards**
 - Wait for full screen render before capturing (2-3 second delay)
 - Ensure stable UI state (no animations in progress)
 - Capture at device's native resolution
 - Use consistent screenshot format (PNG recommended)

6. **Naming Convention**
 
 Use sequential, descriptive filenames:
 - Format: `[sequence]_[screen_category]_[screen_name].png`
 - Example: `01_auth_splash_screen.png`
 - Example: `02_auth_login_screen.png`
 - Example: `03_main_home_screen.png`
 - Example: `04_main_settings_menu.png`

7. **Navigation Documentation**
 For each screenshot, document:
 - Navigation path from app launch
 - Required user actions to reach the screen
 - Any prerequisites (login required, specific state, etc.)
 - Interactive elements present on the screen

8. **Create Comprehensive Documentation**
 
 Generate **`mcp-appium/screen_catalog_android.md`** containing:
 | # | Screenshot File | Screen Name | Category | Navigation Path | Prerequisites | Notes |
 |---|----------------|-------------|----------|-----------------|---------------|-------|
 | 01 | 01_auth_splash_screen.png | Splash Screen | Authentication | App Launch | None | Auto-dismisses after 2s |
 | 02 | 02_auth_login_screen.png | Login Screen | Authentication | After Splash | None | Contains email/password fields |
 
**Note:** 
Link the captured images to the *screen_catalog_android.md* file for easier viewing. When adding the images to the markdown file, ensure the following:

- Display all images at a width of 300px
- Images should scale proportionally.
- Review all screenshots for clarity and completeness
- Verify no duplicate captures
- Ensure all text is readable
- Check for any UI rendering issues or artifacts

## Additional sections:
 - **Screen Flow Diagram**: Visual representation of navigation paths
 - **Screen Categories**: Grouped list of screens by functionality
 - **Coverage Summary**: Total screens captured vs. estimated total
 - **Known Gaps**: Screens that couldn't be captured and why

## Deliverables
- Complete set of numbered, labeled screenshot files
- `mcp-appium/screen_catalog_android.md` with comprehensive documentation
- Summary report with total screens captured and coverage assessment
