# Google Cloud Speech to Custom Search Demo

This sample shows you how to use the [Google Cloud Speech API][speech-api]
to transcribe live audio from your computer's microphone and transmit it to
a custom search API or web browser.

[speech-api]: http://cloud.google.com/speech

## Prerequisites

### Enable the Speech API

If you have not already done so, [enable the Google Cloud Speech
API][console-speech] for your project.

[console-speech]: https://console.cloud.google.com/apis/api/speech.googleapis.com/overview?project=_

### Setup the Custom Search API

[Setup a Custom Search API](http://cse.google.com/manage/all) and make note of
the value in the URL that comes after `cx=`, this is the identifier you will
need when configuring the sample.

### Authentication

This sample uses a service accounts for authentication to the Speech API.

* Visit the [Cloud Console][cloud-console], and navigate to:

    `API Manager > Credentials > Create credentials > Service account key > New
    service account`.
* Create a new service account, and download the json credentials file.
* Set the `GOOGLE_APPLICATION_CREDENTIALS` environment variable to point to your
  downloaded service account credentials:

      export GOOGLE_APPLICATION_CREDENTIALS=/path/to/your/credentials-key.json

  If you do not do this, the streaming sample will just sort of hang silently.

You also must generate a developer API key that will be used with the Custom
Search Engine.

See the [Cloud Platform Auth Guide][auth-guide] for more information.

[cloud-console]: https://console.cloud.google.com
[auth-guide]: https://cloud.google.com/docs/authentication#developer_workflow

### Setup

* Clone this repo

  ```sh
  git clone https://github.com/GoogleCloudPlatform/python-docs-samples.git
  cd python-docs-samples/speech/grpc
  ```

* If you don't have it already, install [virtualenv][virtualenv].

  ```sh
  pip install virtualenv
  ```

* Create a [virtualenv][virtualenv]. This isolates the python dependencies
  you're about to install, to minimize conflicts with any existing libraries you
  might already have.

  ```sh
  virtualenv env
  source env/bin/activate
  ```

* Install [PortAudio][portaudio]. The sample uses the [PyAudio][pyaudio]
  library to stream audio from your computer's microphone. PyAudio depends on
  PortAudio for cross-platform compatibility, and is installed differently
  depending on the platform. For example:

  * For Mac OS X, you can use [Homebrew][brew]:

    ```sh
    brew install portaudio
    ```

  * For Debian / Ubuntu Linux:

    ```sh
    apt-get install portaudio19-dev python-all-dev
    ```

  * Windows may work without having to install PortAudio explicitly (it will get
    installed with PyAudio, when you run `python -m pip install ...` below).

  * For more details, see the [PyAudio installation][pyaudio-install] page.

* Install the python dependencies:

    ```sh
    pip install -r requirements.txt
    ```

* Replace the values for `API_KEY` and `CSE_ID` in `speech_to_search.py` with
  those from the Google Cloud Developer Console and Custom Search Engine you
  created previously.

[pyaudio]: https://people.csail.mit.edu/hubert/pyaudio/
[portaudio]: http://www.portaudio.com/
[pyaudio-install]: https://people.csail.mit.edu/hubert/pyaudio/#downloads
[pip]: https://pip.pypa.io/en/stable/installing/
[virtualenv]: https://virtualenv.pypa.io/en/stable/installation/
[brew]: http://brew.sh

### Troubleshooting

#### PortAudio on OS X

If you see the error

    fatal error: 'portaudio.h' file not found

Try adding the following to your `~/.pydistutils.cfg` file,
substituting in your appropriate brew Cellar directory:

    include_dirs=/usr/local/Cellar/portaudio/19.20140130/include/
    library_dirs=/usr/local/$USER/homebrew/Cellar/portaudio/19.20140130/lib/

## Run the sample

* To run the `speech_to_search.py` sample:

    ```sh
    python speech_to_search.py
    ```

To demo the sample:

* Speak to transcribe what you say and send it to your Custom Search Engine.
  The sample will speak back the first result.
* Say "next" to read the next result.
* Say "quit" or "exit" to quit the sample.

### Deactivate virtualenv

When you're done running the sample, you can exit your virtualenv:

```
deactivate
```
