# MultiUserChat
package com.muc;

fixed String Utils error

    private final Socket clientSocket;

    public ServerWorker(Socket clientSocket) {
        this.clientSocket = clientSocket;
    }

    @Override
    public void run() {
        try {
            handleClientSocket();
        } catch (IOException e) {
            e.printStackTrace();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }


    /**
     *
     * @throws IOException
     * @throws InterruptedException
     * StringUtils error = download apache--extract idea file project structure, add module
     */
        private void handleClientSocket() throws IOException, InterruptedException {
            InputStream inputStream = clientSocket.getInputStream();
            OutputStream outputStream = clientSocket.getOutputStream();

            BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));
            String line;
            while ( (line = reader.readLine()) !=null) {
                String[] tokens = StringUtils.split(line);
                if (tokens != null && tokens.length > 0) {
                    String cmd = tokens[0];
                    if ("quit".equalsIgnoreCase(line)) {
                        break;
                    } else if ("login".equalsIgnoreCase(cmd)) {
                        handleLogin(outputStream, tokens);
                    } else {
                        String msg = "unknown" + cmd + "\n";
                        outputStream.write(msg.getBytes());
                    }

                }
            }
            clientSocket.close();
        }
    }


     
