# AvaloniaLinuxDBusIssue

Minimal example to reproduce the Avalonia DBus issue on Linux.

## Create basic Avalonia app

```
dotnet new avalonia.app -o AvaloniaLinuxDBusIssue
```

## Add sample context menu

https://docs.avaloniaui.net/controls/menus/contextmenu

```xml
<TextBox AcceptsReturn="True" TextWrapping="Wrap" Text="Right-click here">
  <TextBox.ContextMenu>
    <ContextMenu>
      <MenuItem Header="Copy"/>
      <MenuItem Header="Paste"/>
    </ContextMenu>
  </TextBox.ContextMenu>
</TextBox>
```
