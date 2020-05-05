# Solex CC

Solex CC is essentially an "app environment" for companion computers running on MAVLink-based vehicles (planes, copters, rovers, boats, etc).

# Initial idea

In 2015, 3DR released the Solo copter. It used an early version of the Cube flight controller and had an i.MX6 processor on it too, acting as a 
"companion computer". The companion computer was essentially a small Linux machine, and had a Python runtime on it along with libraries for dealing with
MAVLink messages and maintaining an interface to the flight controller.

One of the Solo's features were its "Smart Shots", which were implemented as Python scripts that could be run via an interface on the ground station app.
The Smart Shots were able to automate certain functions on the Solo, allowing it to fly around and take cinematic shots by itself, with less flying skill 
needed on the part of the pilot.

It always seemed that this idea (connected scripts running on the vehicle) could be expanded upon to include more capability, and be easier for a _user_ to
change and augment however they see fit. In essence, you could have an easily-programmable vehicle.

That's where the initial idea for Solex CC came from. As for expanding on the idea, there are several things Solex CC can do that are either not possible with the Solo environment, or somewhat difficult

## Easily install, enable, disable, or remove scripts

On the Solo, installing a new Smart Shot would involve modifying several files on the vehicle to make reference to the new smart shot, uploading your script file(s)
to the appropriate directories, and then modifying the GCS application (3DR Solo app or Solex) with a custom UI flow to make use of the smart shot. This is obviously not impossible, but does involve a lot of moving parts, not to mention cooperation between multiple parties. If all you're after is something simple, or validating an idea you have, this is a lot of work for potentially little reward.

Solex CC's "worker" scripts (the scripts that implement custom functions) all work according to a consistent interface to and from the ground station and vehicle,
so no modifications on Solex CC itself are required for installing a new script. The basic steps are:

1. Write and test the script, giving it a unique ID within the system.
2. Zip it into a .zip file.
3. Open Solex CC's web interface, and click the "Install" button.
4. Select the .zip file you created, and upload it.
5. Wait a few seconds

Your script is now installed and functional.

## UI Customization

In most GCS applications, a major drawback of a flexible scripting environment is that in order to use a new feature, the GCS app has to be modified to take advantage of the feature. Suppose, for example, that you want to write a script to capture output from a sensor attached to the vehicle and log it during a flight, then prompt the user to download that content at the end of the flight. In a Solo-like environment, you'd need to build all of that explicitly. Again, obviously not impossible, but not exactly trivial to do.

In Solex CC, worker scripts can create UI elements themselves. You can define anything from a simple button on an exsiting panel to entire screens, including sliders, entry fields, icons, buttons, check boxes, radio buttons, and so on. The UI definitions also tell Solex (or a similarly-equipped app) what to do when the user interacts with these elements, in which case a worker script becomes part of the GCS app's UI. So, in that case, Solex will behave as if it's designed to perform that specific function, when in reality it's the _vehicle_ controlling the UI for that function.

## Code in any language you like

Solex CC runs on the Node JS environment, so its reasonable to assume that this means you have to write worker scripts in JavaScript or TypeScript, or other languages supported by Node. Technically, this is true; worker scripts are loaded as modules via `require` dynamically at runtime, and their interface to the rest of the system is via JSON messages. The good news is that this part is really simple and easy. If you prefer to write your worker in something else (C, C++, Python, etc), you can do that as well, and provide a "shell" interface from the worker script to your code. The [Examples](https://github.com/kellyschrock/solexcc-example-workers) repository contains a few examples of how this is done.

## Ease of testing

There is a short setup process involved for setting up to test worker scripts. Essentially, you put Solex CC on your computer, in which case it acts as the 
"companion computer" in your testing setup. Set up SITL to act as the "vehicle" in your setup, using any of the vehicle types (Copter, Plane, or Rover). Finally, run Solex on a device on the same WiFi network as SITL on your computer. Start SITL and start Solex CC, then connect to them both with Solex. Now you can develop and test your code without putting any vehicles at risk, and see immediate feedback.

## Runs on any hardware

Solex CC runs on anything that will run Node JS, so it can run on anything from a Pi Zero to a Jetson, to a PC. Strictly speaking, a Pi Zero will run Solex CC, but its performance (as with anything that runs on a Pi Zero) will be noticeably slower than it is on higher-powered devices.


