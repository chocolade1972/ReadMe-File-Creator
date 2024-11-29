# ReadMe File Creator

ReadMe File Creator is a Unity Editor tool designed to simplify the process of creating customizable ReadMe files in markdown (`.md`) format directly within Unity projects. With this tool, developers can easily add project documentation that is both professional and accessible.

## Features

- Create a markdown ReadMe file in any folder via a context menu.
- Automatically formats the ReadMe file with a template, including:
  - Project name and timestamp.
  - Sections like Introduction, Instructions, Examples, and Notes.
- Prompts the user to open the file immediately after creation.
- Fully customizable template to suit your project needs.

## How to Use

1. Install the ReadMe File Creator package in your Unity project.
2. In the Unity Editor:
   - Right-click on any folder in the Project view.
   - Navigate to **Create > ReadMe File** in the context menu.
3. Customize and edit the generated markdown file in your favorite text editor.
4. Use the ReadMe file for documenting important project details.

## Installation

1. Download the package from the Unity Asset Store or the GitHub repository.
2. Import the `.unitypackage` file into your Unity project.
3. The tool will be added under `Assets/Scripts/Editor/`.

## Script Example

The main script is `ReadmeFileCreator.cs`. Below is a simple snippet:

```csharp
using System.IO;
using UnityEditor;
using UnityEngine;

public class ReadmeFileCreator : Editor
{
    [MenuItem("Assets/Create/ReadMe File", false, 81)]
    private static void CreateReadMeFile()
    {
        string path = AssetDatabase.GUIDToAssetPath(Selection.assetGUIDs[0]);
        if (!AssetDatabase.IsValidFolder(path))
        {
            Debug.LogError("Please select a valid folder in the Project view.");
            return;
        }

        string folderName = Path.GetFileName(path);
        string fileName = $"{folderName}.md";
        string filePath = Path.Combine(path, fileName);

        if (!File.Exists(filePath))
        {
            File.WriteAllText(filePath, $"# {folderName}\n\nGenerated on {System.DateTime.Now}");
            AssetDatabase.Refresh();
            Debug.Log($"ReadMe file '{fileName}' created successfully.");
        }
        else
        {
            Debug.LogWarning($"A ReadMe file already exists in the folder: {path}");
        }
    }
}


Contribution
Feel free to fork the repository, submit pull requests, or suggest features. Contributions are welcome!

License
This project is licensed under the MIT License. See the LICENSE file for details.

Support
If you encounter any issues or have suggestions, please open an issue in this repository or contact me directly.

