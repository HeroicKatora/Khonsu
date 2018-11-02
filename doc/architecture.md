# Components

There are at least two layers in the architecture, each with possibly several
independent components communicating via ipc and a common data format or
references to files on disk. This allows each to be created independently and
serves as a simultaneous litmus test for the core values of plain, minimal and
compatible.

In the background, some basic utilities can be pointed at sources of calendar or
task listings to retrieve their information or create a canonical references to
them. Depending on the type of resource, these utilities may also supporting
updating such information, publishing and subscribing to a remote source. For
more information about an `entry`, see <#Entries>. For more information about
interpreting and receiving the output of a backend, refer to <#Backend>.

The core (see <#Core>) is the common source of information for frontends and
backends. It includes configuration management and records information such as
the list of `entry` sources or their credentials. As a consequence, it provides
a single uniform source of truth for viewing calendars and tasks and executing
actions.

A frontend presents the information to the user and takes input to modify the
stored entries, see <#Frontend> for a non-definitive list.

## Entries

An `entry` is the central data structure containing all the information about a
calendar event of a task. Notice that there is no essential difference between
the two and an `event` may be interpreted as either, depending on its collection
of data. The structure is standardized but permits extensions. Unknown content
should be copied but not otherwise processed. (We may consider marking essential
information similar to `png` by naming conventions, resulting in warnings when
encountering particular unknown extensions). Each `event` is laid out as a
simple folder structure:

```text
+ 
+–+log: Contains a folder for previous occurences of this event, each with a log
|       describing what happened.
| …
+–+documents: Contains largely unstructured auxiliary documents but a README.md
|             or similar files may be useful and common for most frontends.
| …
+–?tasks: A file or folder (flat or with subfolders) containing information
|         about individual tasks for this entry. May be referred to in the log
|         for example with a completion note.
\––event.ical: Describes the calendar entry in the RFC 5545 format.
```

Source for events may be (with varying support):
* actual folders
* `zip` or other archive types
* public or authenticated `http` endpoints
* `git` refs/branches/tree-likes

## Backend

Basically, provides `ls`, `find`, `cat`, `open` for `events`. Including
additional operations that largely depend on the concrete implementation.

## Core

In an `xdg-config-dir` or any other configuration directory manages the main
plaintext configuration files and ochestrates data storage in corresponding
`xdg-data-dirs` (or other pointed-to paths). Also translates the core set of
operations from backend to frontend by aggregating data sources and by choosing
some defaults where necessary. Should also contain a plumbing interface for
editing configuration files in order to facilitate doing this in a frontend.

Although mainly used for program interaction, the call arguments and interfaces
should support a user mode not only for debugging but also to aid development or
efficiency when creating new frontends or offering general compabitibility
(plain and compatible).

## Frontend

Interacts with the core in a user compatible way.

* Through a tui (ncurses or similar)
* Through a window system
* Maybe even through a web service?

