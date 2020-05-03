# Solex CC

Solex CC is essentially an "app environment" for companion computers running on MAVLink-based vehicles (planes, copters, rovers, boats, etc).

# Companion Computers FTW

There are a lot of things a MAVLink drone can do without a companion computer. ArduPilot, for example, has a lot of features for interacting with sensors, LEDs, ground-control software, and other systems, all built into the autopilot software. There's even a scripting interface built into it, using the Lua language.

But what if you have an idea for something else? Maybe it's connecting to a sensor that ArduPilot doesn't support. Maybe you need to use a sensor for some purpose other than what ArduPilot would use it for. Maybe you want to make your vehicle do something that ArduPilot doesn't do already. Maybe you want more control over something than you would get via ArduPilot's interface. Maybe you're just experimenting with an idea and want to see results quickly to validate some idea you have. You have choices in this case.


## The direct route

The direct route follows a path similar to this:

1. Download the ArduPilot source code.
2. Figure out where to make the modifications you want in the 4000+ files in the source tree.
3. Make those modifications and test them.

Assuming your idea is appropriate for inclusion in ArduPilot itself (few of them are), you may want to see about getting it merged into the main ArduPilot source tree. In that case, you can undertake the process of getting your modification merged. Start by locating an "influencer" on the ArduPilot team, and they can walk you through the process of selling your idea to whoever is tasked with reviewing your modification and maybe merging it. You can reach out to them on Skype, something called "mumble", or by posting a message in a forum somewhere and hoping it sparks a discussion big enough to get the attention of your chosen influencer. Then you can make a pull request, which they'll help you create so it's exactly right and less likely to get rejected. Next comes the review process, which can span multiple months. (These people are busy, in part because of so many people using this "direct" route for their ideas.) So it's a good idea to periodically check on the progress of your PR and see if anyone has looked at it and perhaps remind someone that the PR is still in need of review. Fail to do this, and your modification may linger for over a year and finally be abandoned. An alternative is to pay one of the ArduPilot developers to implement your idea for you. 

In any case, you may reach a point where your feature requires some kind of new user-interface element in a GCS in order to use it. In that case, once your idea has reached this point, you can alter your GCS to include access to the new feature.

## The "Solex CC" route

With Solex CC, the intention is for the path from "idea" to "it actually works" to be shorter. The basic steps are:

1. (First time only) follow the steps in "Hardware setup" below to install a companion computer on your vehicle. Be prepared to spend at least $35 in this step.
2. Write a worker script to provide an interface between your chosen hardware, the autopilot, and the GCS. This can be anything, really... some kind of sensor, an actuator, a specific camera, or just something to control the vehicle itself in a specific way. You can interface with the vehicle, any external hardware supported by your companion computer, and you can also create user-interface elements for specific screens in an appropriately-instrumented GCS (such as Solex).
3. Install the worker on your vehicle via Solex CC's web interface. 
4. Connect to your vehicle via Solex or some other GCS with SolexCC support (if not already connected).
5. Use the new UI elements that automatically appear in the GCS to make use of your new features.
6. Test and debug your feature using Solex CC's web interface, or various testing-related features are in Solex.

When you've finished your experiment and decide that you don't need it anymore, you can disable or remove the worker. And it, along with all related functions, disappears. Just re-enable it when you need it again.

The difference in time and effort between these approaches is substantial. The direct route can take a while. The Solex CC route can take minutes to hours, depending on how complex and involved your feature is.

Overall: If you want to use your vehicle in ways beyond what its creators intended without a lot of messing around, this is a pretty handy way to do it.

# Hardware Setup

Solex CC can run on anything that can handle a Node JS environment. This includes everything from a $35 Raspberry Pi to full-blown server-sized PC. A Raspberry Pi is a good place to start. Even a Pi Zero will work, but it's really slow. A Raspberry Pi 4 is a better choice. It's also been run on a variety of NVIDIA devices (Jetson, Nano), which is useful if you need more speed.

Once you get a copy of Solex CC, you can follow the tutorials for setting it up.

# Examples

There are a lot of examples about how you might write a worker to do various things, in the [Examples Repo](https://github.com/kellyschrock/solexcc-example-workers).


