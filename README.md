# todo App - a demonstration of low latency stateful data serving and edge functions
A stateful serverless edge function (running on StackPath (https://www.stackpath.com/products/serverless-scripting/)  for serving low latency data from Macrometa's global database (www.macrometa.co) showcased as a "ToDo List App"

Try the app - https://todo.edgezilla.io/  (use the developer tools in chrome to measure network time for end to end latency - from click to edge function (on StackPath) to DB on Macrometa's service and back)

This is a simple TO DO app based on a tutorial by cloudflare (CF) on using CF Workers (https://workers.cloudflare.com/) and CF KV Store (https://developers.cloudflare.com/workers/reference/storage)

I found CF KV Store to be extremely slow for something that claims low latency and global data distribution (140 milliseconds for a PUT - come on!!).  Also CF KV Store is eventually consistent and that means global edge apps CANNOT trust state as it might be stale (Eventual Consistency only makes a liveness gaurantee)

So instead Ive re-implemented this to use Macrometa's global database (which provides a KV, DocDB, Graphs, Time series, pub/sub, streams and event processing). Macrometa DB is extremely low latency and offers a better consistency model based on using CRDTs (https://www.macrometa.co/technology). The underlying tech has been heavily scrutinized at places like High Performance Transaction Systems (HPTS 2019).  The Macrometa DB is globally distributed across 100s of locations at CDN scale and delivers stateful data handling to containers, lambdas, serverless functions and more. 

The current version in this repo has 2 limitations:
1. Currently hardcoded to a single POP in SF (using a limited access account) - I'll fix this with a global URL at some point.
2. Ive not implemented login - so the JWT will expire.  Please reach out to Macrometa (info@macrometa.co) if you want your own account. Also I leave the implementation of proper auth to the reader as an exercise. 

Future-
Post a version that works on CF that uses Macrometa and CF workers (instead of CF KV)
Post a version that works with AWS Lambda @ Edge on CloudFront

