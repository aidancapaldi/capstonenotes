Aidan Capaldi

#### Research Items and Questions: 
- Look into a viable tech stack for the front end of the app

##### Web Application Stack and Design 
We can make a viable web application using `React.js`. I've had some experience working with it in the past, and could absolutely do so again!

I'm thinking that we need the following setup: 
- 9 (or 6) axis central IMU 
- Smaller children IMU's or accelerometers on the skates themselves
- A datalogger for the IMU data

We should be interested in IMUs on the skates to provide tilt data needed for the calculation of inside versus outside edge of skating.

A datalogger would allow for the information coming into the sensors to be relayed in a very web-friendly format. Note the following from a [viable datalogger](https://www.sparkfun.com/products/20594):
```
The SparkFun DataLogger IoT - 9DoF is a data logger that comes preprogrammed to automatically log IMU, GPS, and various pressure, humidity, and distance sensors. All without writing a single line of code! The DataLogger automatically detects, configures, and logs Qwiic sensors. It was specifically designed for users who just need to capture a lot of data to a CSV or JSON file and get back to their larger project. Save the data to a microSD card or send it wirelessly to your preferred Internet of Things (IoT) service!
```

We can use [Node and NPM](https://medium.com/front-end-weekly/a-beginners-guide-building-front-end-applications-with-react-1f0d3e75c0a7) to easily and readily deploy a locally-hosted draft of the site. We may just be interested in doing this for the presentation and easy access of data (e.g. we want to update elements on the website as we go). As long as the datalogger works to provide JSON output, we can use that readily in React. 

We can also elect to freely publish the web application to [GitHub Pages](https://pages.github.com/). This site allows for extremely simple and robust deployment of developed web apps to a free hosting environment. 
The webpage should display the mapped path from a bird's-eye view of the skate accelerometers, and then highlight in contrasting colors which edge of the skate (calculated from tilt). 

We can use [HTTP Polling](https://askus.how/real-time-updates-in-your-react-application/) or a selection of other options shown in that guide to provide this tracking data in real time. 