# Deploy Configuration

The deployment method determines how to ship your experiment to your participants (if at all)
and how to process its data. For development, you will want to use the `debug` mode, which
shows the data collected from the current execution of the experiment in the browser at the end
of the experiment. 

To actually collect data from participants, \_magpie uses the magpie server app
to store the data in a data base (and possibly to manage allocation of participants to
different variants of your experiment). You therefore need to have a running instance of the server app, either online or locally, as described in [the server app section on installation](/02_using_the_server_app/01_installation/).


There are three deployment modes to collect data via the \_magpie server app (to be detailed below):

1. The `directLink` mode allows participants to work on your experiment simply by following a link.
2. The `MTurk` mode is used to recruit participants via [Amazon's Mechanical Turk](https://requester.mturk.com/).
3. The `Prolific` mode is used to recruit participants via [Prolific](https://prolific.ac).

All of these methods require that you have initialized a database on the \_magpie server app, as described [here](/02_using_the_server_app/02_use/). You need the `experimentID` (a running number) which the server app creates for your experiment, as well as the URL (possibly local) of your experiment.

Unless you run your experiment strictly locally on your own (lab) computer(s), you also need to
launch the experiment as a website on some hosting service. A possibility for doing so is
described in the section on [hosting on
Netlify](/03_deploying_experiments/02_hosting_on_netlify/).

## Changing deploy information

Deployment information needs to be given during the initial creation of the \_magpie-object (e.g., in file `06_main.js` of the [Departure Point](https://github.com/magpie-ea/departure-point)), by setting the properties of the `deploy` object, as shown below:

```javascript
 magpieInit({
        ...
        deploy: {
            experimentID: "INSERT_A_NUMBER",
            serverAppURL: "https://magpie-demo.herokuapp.com/api/submit_experiment/",
            // Possible deployment methods are:
            // "debug" and "directLink"
            // As well as "MTurk", "MTurkSandbox" and "Prolific"
            deployMethod: "debug",
            contact_email: "YOUREMAIL@wherelifeisgreat.you",
            prolificURL: "https://app.prolific.ac/submissions/complete?cc=SAMPLE1234"
        }
        ...
    });
```

None of these fields matter for the `debug` mode. But for any of the other modes, you should specify appropriate information to the following fields:

+ `contact_email` should contain an appropriate email address which will be displayed in an alert box in case of errors, so your participants can directly reach out to you.
+ `experimentID` must contain the ID the \_magpie server app provided for your experiment when created it online (see the [section on server app use](/02_using_the_server_app/02_use/#creating-new-experiments) for more information).
+ `serverAppURL` is the URL (possibly local) to your server app instance which handles the data (see the [section on server app use](/02_using_the_server_app/02_use/#creating-new-experiments) for more information).
+ `prolificURL` needs to be specified only if you use the `Prolific` deploy mode. In that case you need to enter here the return URL given to you when you create your experiment on the Prolific web site (see information below).
