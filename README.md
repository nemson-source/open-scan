This is a simple node.js newtwork scanner that will loock for responding ip's and open ports

to use it make shure that you have node.js installd if not you can install it here https://nodejs.org/en/

to use unzip the file named node_modules then start the file scan.bat at the end of the scan it will open and creat the following files
responding.txt

openport.json

nonresponding.txt (this file will not automaticli open)

log.txt (this file will not automaticli open)


Features are
gives the responding ip's with Respons time
gives the non responding ip's
and it gives the open ports on every responding device with the ports usage

to change the IP open the index.js file and change the IP in this (defaut ip is 192.168.0.1)

```
for (let i = 1; i <= 255; i++) {
  const host = `192.168.0.${i}`;

  ping.promise.probe(host)
    .then(res => {
      if (res.alive) {`
        responding.push(`${res.host}: ${res.time} ms`);
        scanPorts(res.host);
      } else {
        nonResponding.push(res.host);
      }

      if (responding.length + nonResponding.length === 255) {
        printResults();
      }
    });
}
```
to change the port scan range change this code (defauld port range is 1000)
```
const scanPorts = (ip) => {
  for (let port = 1; port <= 1000; port++) {
    const socket = new net.Socket();

    socket.on('error', (err) => {
      socket.destroy();
    });

    socket.on('connect', () => {
      openPorts[ip] = openPorts[ip] || [];
      openPorts[ip].push({ port: port, function: getPortFunction(port) });
      socket.end();
    });

    socket.connect(port, ip);
  }
};
```
