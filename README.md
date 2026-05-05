# AvaloniaLinuxDBusIssue

Minimal example to reproduce the Avalonia DBus issue on Linux.

## Create basic Avalonia app

```
dotnet new avalonia.app -o AvaloniaLinuxDBusIssue
```

## Add sample context menu

https://docs.avaloniaui.net/controls/menus/contextmenu

```xml
<Window>

  <TextBox AcceptsReturn="True" TextWrapping="Wrap" Text="Right-click here">
    <TextBox.ContextMenu>
      <ContextMenu>
        <MenuItem Header="Copy"/>
        <MenuItem Header="Paste"/>
      </ContextMenu>
    </TextBox.ContextMenu>
  </TextBox>

</Window>
```

## Add logging callback

https://docs.avaloniaui.net/docs/app-development/logging-errors-and-warnings#logtodelegate

```csharp
public static AppBuilder BuildAvaloniaApp()
    => AppBuilder.Configure<App>()
        // ...
        .LogToDelegate(Console.WriteLine);
```
