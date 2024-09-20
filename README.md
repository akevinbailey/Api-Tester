# Api-Tester

**PURPOSE:**

Api-Tester is an open-source application used to test the throughput and latency of a REST service.  It currently
just supports the GET method but the code can easily be modified to test other HTTP methods.

**DESCRIPTION:**

Api-Tester will take the total number of calls and divide them between the given number of threads.  Each thread will
execute its assigned number of calls in a sequential manner.  There are five versions of Api-tester.  Each version is
written in a different language (C, Go, Java, Python, and Rust), but provide the same functionality.  The only
exception is the Java version does not support `-keepConnectOpen`, because the HttpClient class automatically
reads the request body, and reuses or closes the connection.  The usage is as follows:

	Usage:
	api-tester [URL] [arguments]
	Required arguments:
	  [URL]                   - Server URL.
	Optional Arguments:
	  -totalCalls [value]     - Total number of calls across all threads. Default is 10000.
	  -numThreads [value]     - Number of threads. Default is 12.
	  -sleepTime [value]      - Sleep time in milliseconds between calls within a thread. Default is 0.
	  -requestTimeOut [value] - HTTP request timeout in milliseconds. Default is 10000.
	  -connectTimeOut [value] - HTTP request timeout in milliseconds. Default is 20000.
	  -reuseConnects          - Attempts to reuse the connections if the server allows it.
	  -keepConnectsOpen       - Force a new connection with every request (not advised).
	Help:
	  -? or --help            - Display this help message.

**WARNING:**

Api-Tester has the potential to make your computer unresponsive by maxing out all of its CPU cores.  This is
especially dangerous when running Api-Tester on a remote machine, as the remote session could be frozen until the
test is finished.  Be cautions when leaving `-seepTime` set to `0` and setting `-numThreads` to more than your CPU
cores.  Also, setting `-keepConnectsOpen` can cause the computer run out of ports or make it unresponsive due
to excessive resource utilization.
