# Design Decisions

## Type of GUI Applications

The application's features matter, not its GUI library. What applications are missing?

I switched from Windows to MacOS many years ago. There were many applications that needed to be found and installed before the migration. There are Text Editor, Office, FTP client, SQL client, Git client, Video player, etc.

I recently switched from MacOS to Debian (Linux). By this time, almost all applications have become web-application. There are VS Code, Slack, etc. Most applications exist as SPAs (Single Page Application) on websites. There are Office, GMail, YouTube, etc. Everything is ok with them.

But it became very uncomfortable for me to think while working with applications. I have to make sure the app is ready before writing anything. It disturbs me, interrupts my work. I dream of an application that instantly reflects the result of my actions, instantly shows information. To be able to create without interruption.

My requirements for the application being developed:

- Fast like a native app. Both the reaction to the event and the initial launch must be instantaneous.
- Cross-platform is preferred. Linux and MacOS should be supported.
- The application must display text, images, charts.
- Multiple windows must interact with the user at the same time.

Not required for implementation:

- The app may not play video and audio clips.
- The application may not draw 2D or 3D graphics.

## GUI Application Programming Language

To be fast:

- Compiled.
- Minimal run-time overhead.

General requirements:

- High level abstractions.
- Minimal vendor lock.

Winners at this stage: C++, Rust, Go, Haskel maybe.

C++ is very close. C++ is complex too. It's suitable if you can select which language subset to use. There are issues with concurrency and cross-platform building.

When development started, Rust was not as reliable as Go. Maybe suitable for prototyping at the moment.

Haskell has been used in prototyping. I stopped testing when I needed to completely rewrite the Haskell code for the next version.

By the way: the winner is Go.

## API set of GUI library

The requirements:

- Facade pattern for masking complex components behind an API. Also a starting point for future refactorings.
- Minimum set of objects and methods in the API.
- Simple and clean application code for event handling.

One comment about form designers and widgets. In fact, it is useful in many cases. However, out-of-the-box widgets require the use of event-driven programming paradigm. In the first step, I will try to avoid form designers and widgets.

## Base low-level GUI implementation

In fact, a lot of code is required under the hood, for example, to implement text rendering. Rasterize a True-Type font to a bitmap, redraw a bitmap on demand, and so on.

For the first versions, it's easier to use a well-tested low-level library. In fact, you will have to choose between GTK and QT.

QT is not the cheapest choice. GTK is the winner.
