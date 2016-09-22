# xiblint

The `xiblint` script will test .xib and .storyboard files for compliance with best practices and team policies.

The error message contain the location within the XML files, and if possible, the Object ID of the relevant object.
The Object ID can be used in conjunction with Xcode's Find in Workspace feature to jump to the problematic object
or view in the .xib or .storyboard file.

## Rules

- accessibility_format

  Checks for incorrect use of Lyft extensions `accessibilityFormat` and `accessibilitySources`.

- automation_identifiers

  Makes sure that interactive views have accessibility identifiers, to support testing through UI Automation.

- accessibility_labels_for_image_buttons

  Checks for image buttons with no accessibility label.
  In this case, VoiceOver will announce the image asset's name, which might be unwanted.

- accessibility_labels_for_text_with_placeholder

  Checks for text fields and views with a placeholder and no accessibility label.
  This addresses common confusion about `placeholderText` coming instead of `accessibilityLabel`.

- automation_identifiers_for_outlet_labels

  Checks for labels with outlets into a view controller that have no accessibility identifiers.
  Labels with outlets might get dynamic text, and therefore should be accessible to UI testing.

- simulated_metrics_retina4_0

  Ensures simulated metrics are for the iPhone SE, which is currently the smallest display profile.

- no_trait_variations

  Ensures Trait Variations are disabled.

- autolayout_frames

  Checks for ambiguous and misplaced views.

## Usage

To list the rules and their description, run `xiblint -h`.

Place a configuration file named `.xiblint.json` into the root of your source repository. A sample configuration file would be:

```json
{
  "rules": [
    "accessibility_format",
    "autolayout_frames"
  ],
  "paths": {
    "Pods": {
      "rules": []
    },
    "InaccessibleFeature": {
      "excluded_rules": [
        "accessibility_*"
      ]
    }
  }
}
```

Then simply invoke `xiblint` in that directory.