<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>How to Run a Server and Access from Another Network</title>
</head>
<body>
    <h1>How to Run a Server and Access it from Another Network</h1>

    <h2>1. Run the Spring Boot Server</h2>
    <ol>
        <li>Run the Spring Boot application using the following command:
            <pre><code>./gradlew bootRun</code></pre>
        </li>
        <li>Ensure the server is running on <code>localhost:8080</code> by testing it in a browser:
            <pre><code>http://localhost:8080</code></pre>
        </li>
    </ol>

    <h2>2. Find Your Internal IP Address</h2>
    <ol>
        <li>Open the command prompt and run:
            <pre><code>ipconfig</code></pre>
        </li>
        <li>Find the <b>IPv4 Address</b>, e.g., <code>192.168.219.103</code>.</li>
    </ol>

    <h2>3. Find Your Public IP Address</h2>
    <ol>
        <li>Open a browser and go to <a href="https://ip.pe.kr" target="_blank">ip.pe.kr</a>.</li>
        <li>Note the public IP address, e.g., <code>49.165.191.3</code>.</li>
    </ol>

    <h2>4. Configure Port Forwarding</h2>
    <ol>
        <li>Login to your router's management page (usually <code>http://192.168.219.1</code>).</li>
        <li>Go to the <b>NAT/Port Forwarding</b> section.</li>
        <li>Add a new rule with the following details:
            <ul>
                <li><b>Service Port:</b> 8080 - 8080</li>
                <li><b>Protocol:</b> TCP</li>
                <li><b>Internal IP:</b> 192.168.219.103</li>
                <li><b>Internal Port:</b> 8080</li>
            </ul>
        </li>
        <li>Save the settings and reboot the router if necessary.</li>
    </ol>

    <h2>5. Open Port 8080 in Windows Firewall</h2>
    <ol>
        <li>Search for <b>Firewall</b> in the Windows search bar and open <b>Advanced Security Settings</b>.</li>
        <li>Add a new inbound rule:
            <ul>
                <li><b>Rule Type:</b> Port</li>
                <li><b>Protocol:</b> TCP</li>
                <li><b>Port Number:</b> 8080</li>
                <li><b>Action:</b> Allow the connection</li>
                <li><b>Profile:</b> Domain, Private, Public</li>
                <li><b>Name:</b> Spring Boot 8080</li>
            </ul>
        </li>
    </ol>

    <h2>6. Test Connection from Another Network</h2>
    <ol>
        <li>Ensure the client device is on a different network (e.g., mobile data).</li>
        <li>Access the server using your public IP and port:
            <pre><code>http://49.165.191.3:8080/api/users/view</code></pre>
        </li>
    </ol>

    <h2>7. Network Logic</h2>
    <ul>
        <li><b>Client to Router:</b> The client sends a request to the router using the public IP.</li>
        <li><b>Router to Server:</b> The router forwards the request to the internal server based on the port forwarding rules.</li>
        <li><b>Server to Client:</b> The server processes the request and sends a response back through the router.</li>
    </ul>

    <h2>8. Additional Notes</h2>
    <ul>
        <li>If the public IP changes frequently, consider using a static IP or a DDNS service.</li>
        <li>Disable port forwarding when not in use to enhance security.</li>
    </ul>
</body>
</html>
