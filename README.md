# SPMU

SPMU is an experimental replacement for the GNU-based userspace used in standard GNU/Linux systems, designed to accomodate
distributed computing tasks as conveniently as possible.
It is currently a work in progress, and should not be considered functional until this readme is updated to state the contrary.

## Why the name?

SPMU (pronounced "spuh-moo") is a recursive acronym, following the example of many GNU packages.

Until the system actually works, the name can be considered as "SPMU's Pretty Much Unusable".
At some point this may change to "SPMU Pubsub Management Userspace" if the current maintainer can actually get it to work.

## How does it work?

(It doesn't.  Everything in this section is currently theoretical.)
SPMU acts as a wrapper around the Linux Kernel API, allowing system calls from userspace processes to be rerouted to different machines if necessary.
By enabling the sharing of hardware resources, the virtualization layer presents a single unified userspace across an arbitrary number of machines.
This includes a single filesystem tree, a single database of available programs and libraries, and a general detachment from any need to know about 
the devices in use.  All disk data can be written across multiple storage devices automatically for data backup and optimized retrieval times, with 
per-subtree configuration available. Package management is global across all machines, using a modified version of Portage to automate installation
on different hardware.  Portage packages should be modified to add a set of tags describing the limits to the capabilities of the package, determined
at compile time based on the machine's USE flags.  These tags are used to determine which machines can satisfy the requirements for a given job.

To facilitate simple automation of process pipelining, SPMU uses Turtle as its shell scripting language.  Turtle is a simple, dynamically-typed, and
functional language, specialized for interacting with processes for purposes such as metadata manipulation, task distribution configuration, and 
dynamic data pipeline definition.  Turtle will purposely be kept very small in both grammar and purpose, as atomic process creation (i.e. any process
that operates directly on data rather than consisting entirely of other processes) should be handled by existing tools such as Bash.


## Is this a replacement for all core GNU tools?

No.  SPMU will make heavy use of existing software such as GCC, binutils, bash, etc.  The core difference will be in how these (and other) packages
are made available to users.  SPMU will rely on source-based distribution of packages, allowing for native package installations across multiple machines.
SPMU packages will require some amount of metadata used to determine if the underlying installation of a package can actually satisfy the requirements 
of a given process at runtime.

## Is this necessary?

Probably not.  It is likely that there are far better approaches to distributed computation than this.  SPMU is an 
academically-motivated project, an exercise exploring the challenges of developing system architecture around preexisting software.
