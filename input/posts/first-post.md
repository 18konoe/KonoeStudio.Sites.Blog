Title: First Post
Published: 1/1/2016
Tags: Introduction

---

This is my
first post!

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

<?# Gist 34dfb637dc055658611db19adc31a982 DependencyInjectionModel.cs 3-11 3 Caption="INoMeanInterface, NoMeanClass" /?>

<?# YouTube woUcH7G3MAw /?>

<?# Twitter 1228911373318443008 /?>

# Header 1 {#header1}

[Link](#header1) back to header1

# Header 2 {.my-class}

# Le Site {lang=fr}

This is an example[^3] of footnote usage.

[^3]: An example footnote.

1. Level 1
   i. Level i
   a. Level a

- [ ] a task list item
- [ ] list syntax required
- [ ] normal **formatting**
- [ ] incomplete
- [x] completed

![Rick Roll](https://www.youtube.com/watch?v=dQw4w9WgXcQ)

> This is a blockquote
> ^^ This is a ""citation for name""

:::{.alert .alert-info}
This is a Bootstrap alert.
:::

""Tractatus Logico-Philosophicus"" was first published in 1921.

""ハゲ太郎"" was first published in 1921.

\*[HTML]: Hypertext Markup Language

Later in a text we are using HTML and it becomes an abbr tag HTML

<?# Lightbox ../img/IMG_20200106_100330.jpg Title="Test Title" /?>

| Right | Left | Default | Center |
| ----: | :--- | ------- | :----: |
|    12 | 12   | 12      |   12   |
|   123 | 123  | 123     |  123   |
|     1 | 1    | 1       |   1    |
