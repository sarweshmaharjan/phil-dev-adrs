# Sprout 90 Day Bundle



# Testing Flow:

1. Generate an order for Sprout NDC with the following settings. 
  1.1 Stages: Delivered
  1.2 Quantity, Days of Supply, and Package Size: 30 
  1.3 VPS Claim Type: Insurance Claim
  1.4 BestRx Claim: Approved
  1.5 Payment Type: Commerical
  1.6 Insurance Type: Non Caremark
  1.7 Coupon Enrollment: Enrolled
  1.8 Pa Stage: Prior Auth Denied

2. Open the Order and modify the patient details to add the phone number as: (111) 111-1111

3. Copy the order Number and go to Thanos tools "Update Rx/Order State" and search for that order number. 

4. Modify below fields. 
  4.1 otherCoverageCode: 3
  4.2 refillDate: today + 1 day.

5. Check if it has been updated.

6. Trigger job: REFILL_SKIP_NOTIFICATION to URL: `http://localhost:8888/_internal/workflow/v1/trigger-job`
  6.1 payload
        ```json
         {
    "jobName": "REFILL_SKIP_NOTIFICATION",
    "params": {"TimeZone":"America/Los_Angeles"}
}
        ```

```txt
Trick:

1. Make func IsEligibleFor90daysBundle(rx *data.Prescription) bool {	return true }
2. func sendRegularSkipRefillNotification(ctx context.Context, rx *data.Prescription) bool {
if mgr.CanSendSMS() || true {}}

Making both true, will ensure you get comments on the link while on local testing. 
```

7. refresh page. 

8. in the comment you will see something along the lines of
```text
SMS TEXT:- Steve: Your Addyi prescription refill will be delivered on 01/26. Go to your account at http://localhost:3000 for more info or to make any changes. Did you know? You now qualify for a special 90 day pricing! Click here to claim now: http://localhost:3000/sprout-offer/BRGyVir0v4Mp
````

9. Click on the url. `http://localhost:3000/sprout-offer/BRGyVir0v4Mp`. It will open Phil-me, password is "phil123"

10. Click on "Switch to 90 days" 

11. refresh page

12. on the left side sidebar, search for the refill date. Click on "Refill Now" 

13. Type anything. 

14. 
