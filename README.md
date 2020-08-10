# todo App - a demonstration of low latency stateful data serving and edge functions
A stateful serverless edge function (running on StackPath (https://www.stackpath.com/products/serverless-scripting/)  for serving low latency data from Macrometa's global database (www.macrometa.co) showcased as a "ToDo List App"

Try the app - https://todo.edgezilla.io/  (use the developer tools in chrome to measure network time for end to end latency - from click to edge function (on StackPath) to DB on Macrometa's service and back).  

Depending on where you physically are (city, state, country) you will be routed to the closest StackPath Edge PoP where the serverless function will run to generate the HTML and serve data from the closes Macrometa database PoP.  In contrast to current web architectures where the back end (functions/lambdas or containers and the database) run in one region, the app exploits global distribution and exeuction of functions (stackpath) and data (macrometa database). The end to end latency should be no more than 50-60ms per request for serving database requests via the function to your browser. 

Prior art and motivation

This is a simple TO DO app based on a tutorial by cloudflare (CF) on using CF Workers (https://workers.cloudflare.com/) and CF KV Store (https://developers.cloudflare.com/workers/reference/storage)



Limitations

The current version in this repo has the following limitations:
2. Ive not implemented login - so the JWT will expire.  Please reach out to Macrometa (info@macrometa.co) if you want your own account. Also I leave the implementation of proper auth to the reader as an exercise. 

Future work:
1. Post a version that works on CF that uses Macrometa and CF workers (instead of CF KV) - (almost completed)
2. Post a version that works with AWS Lambda @ Edge on CloudFront (not yet started)

