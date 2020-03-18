Docker images can eat up a bunch of space. If you want your images to be on a separate harddrive from C:, first set Hyper-V to use a different drive.

Before installing Docker, Hit start, type `Hyper-V Manager`.

In the global Actions pane of Hyper-V Manager click Hyper-V Settings…
Under Virtual Hard Disks change the location from the default to your desired location, for example: `D:\Hyper-V\Virtual Hard Disks`
Under Virtual Machines change the location from the default to your desired location, and click apply.
Click OK to close the Hyper-V Settings page.

Now Install Docker and it should install in the extra drive.
