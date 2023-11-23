To integrate **dump978-fa** with **readsb** and pass data between them,
you\'ll need to follow a series of steps. Here\'s a detailed guide on
how to achieve this:

**1. Start dump978-fa with Raw or JSON Output**

First, you need to start **dump978-fa** so that it outputs data to a
network port. You can use either the **\--raw-port** or **\--json-port**
option depending on what data format **readsb** can process. I\'ll use
the **\--raw-port** for this example:

```bash
./dump978-fa \--sdr driver=rtlsdr,serial=00000001 \--raw-port 30978
```
This command starts **dump978-fa** with your specified SDR settings and
makes it listen on port 30978 to provide raw UAT messages.

**2. Configure readsb to Receive Data**

Next, you\'ll configure **readsb** to receive the data from
**dump978-fa**. If **readsb** is capable of processing raw data from
**dump978-fa**, you can use the **\--net-connector** option to set up a
connection to the port where **dump978-fa** is outputting its data:

```bash
readsb \--net-connector 127.0.0.1,30978,raw_in
```
This command instructs **readsb** to establish a network connection to
**127.0.0.1** on port **30978**, expecting raw data as input.

**3. Test the Configuration**

After configuring both **dump978-fa** and **readsb**, you should test
the setup:

-   Start **dump978-fa** using the command from step 1.

-   In another terminal, start **readsb** using the command from step 2.

-   Monitor the outputs of both programs to ensure that data is being
    transmitted from **dump978-fa** and received by **readsb**.

**4. Script Automation**

If you want to automate this setup in a script (such as modifying the
**readsb** installation script), you would follow these steps:

-   **Add Commands to Start dump978-fa**: Include the command to start
    **dump978-fa** with network output in your script.

-   **Modify readsb Startup Options**: In the same script, modify the
    **readsb** start-up command to include the **\--net-connector**
    option, pointing to the **dump978-fa** output port.

Here\'s an example snippet that you might include in a bash script:

```bash
\# Start dump978-fa with raw output ./dump978-fa \--sdr
driver=rtlsdr,serial=00000001 \--raw-port 30978 & \# Wait for dump978-fa
to initialize sleep 10 \# Start readsb and connect it to dump978-fa
readsb \--net-connector 127.0.0.1,30978,raw_in &
```

This script starts **dump978-fa** in the background, waits for it to
initialize, and then starts **readsb**, also in the background,
connecting it to the **dump978-fa** output.
