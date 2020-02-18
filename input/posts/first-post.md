Title: First Post
Published: 1/1/2016
Tags: Introduction

---

This is my first post!

Test code:

```csharp
public class SafeDevInfoHandle : SafeHandle
{
    public INativeHelper Helper { get; }
    public SafeDevInfoHandle() : this(new NativeHelper())
    {
    }

    public SafeDevInfoHandle(INativeHelper helper) : base(IntPtr.Zero, true)
    {
        Helper = helper ?? throw new ArgumentNullException($"{nameof(helper)} is null");
    }
    public SafeDevInfoHandle(IntPtr existingHandle, INativeHelper helper) : base(existingHandle, true)
    {
        Helper = helper ?? throw new ArgumentNullException($"{nameof(helper)} is null");
    }
    protected override bool ReleaseHandle()
    {
        return Helper.ReleaseSafeDevInfoHandle(handle);
    }

    public override bool IsInvalid => handle == IntPtr.Zero;
}
```

<?# Gist 1bef37990c863bac23e6a4be06e4ac62 /?>

<?# YouTube woUcH7G3MAw /?>

<?# Twitter 1228911373318443008 /?>
