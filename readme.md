##Running AB Testing on OpenShift

**Steps**

* Using Web Console create a new-app with name `app-a`. Go to advanced options and uncheck the route creation option so that the app does not create a route. We will add the route later.
* Add a route by clicking on the `Create Route` option next to service `app-a`. Give a common name for the route as it will frontend multiple versions of the application eg: appab-abdemo.apps.testv3.osecloud.com
*  Annotate the route to use `roundrobin` load balancing method

``` 
oc annotate route/appab haproxy.router.openshift.io/balance=roundrobin
```

* Test your app and check the results
* Edit the code to make some changes
* Using web console add a new-app with name `app-b` without route. Verify that service `app-b` got created
* Now edit the route to split traffic between services `app-a` and `app-b`. You can change the percentages and test
* Test using `curl` from your workstation

```
for i in {1..20}; do curl http://appab-abdemo.apps.testv3.osecloud.com/; echo ""; done
```

