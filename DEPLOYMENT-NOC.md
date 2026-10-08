# Deploy NOC Lemhannas

Build the frontend from the same source revision that will run on the server. The
production build now emits several hashed JavaScript and CSS files; deploy the
entire `dist` directory, including every file under `dist/assets`, rather than
copying only `index.html` or the main JavaScript file.

```sh
npm ci
npm run build
npm start
```

Before starting the service, verify that each `/assets/...` path referenced by
`dist/index.html` exists under `dist`. If a build fails, do not restart the
running service with a partial `dist` directory.

The NOC page and Uptime Kuma dashboard are served by the same application on
port `3001`:

- `/dashboard`
- `/noc`

Keep the existing website on its current port and configuration. Only deploy
this application to port `3001` if that port is assigned to the Uptime Kuma
service. Do not stop or replace another application that owns the port.

After deployment, verify `/dashboard`, `/noc`, and the JavaScript/CSS asset URLs
referenced by the current `dist/index.html` return successfully from port `3001`.
For a safe update, build the complete release first, then replace the application
files and restart only its Uptime Kuma service.
