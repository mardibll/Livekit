<script>
  import { Peer } from 'peerjs';
  import { onMount } from 'svelte';
  import { createEventDispatcher } from 'svelte';
  let codeid = "";
  let videocurrent;
  let videoEl;
  let youid = "";
  const dispatch = createEventDispatcher();

  const peer = new Peer();

  // GET YOUR ID
  peer.on('open', (id) => {
    youid = id;
    console.log(id);
  });

  // HANDLE CONNECTION
  peer.on('call', async (call) => {
    // Open webcam
    await navigator.mediaDevices.getUserMedia({
      video: true,
      audio: true,
    }).then((stream) => {
      call.answer(stream);
      call.on('stream', renderYouWebcam);
      videocurrent.srcObject = stream;
      videocurrent.play();
    }).catch(err => console.log('Error message: ' + err));
  });

  // RENDER YOUR WEBCAM HERE
  const renderYouWebcam = (stream) => {
    // console.log(stream);
    videoEl.srcObject = stream;
    videoEl.play();
  };

  // CONNECT TO FRIEND
  const connectToFriend = async () => {
    const conn = peer.connect();
    console.log(conn,"HALOOO");
    // conn.on('data', (data) => {
    //   console.log('New data ' + data);
    // });

    // conn.on('open', () => {
    //   conn.send('hi');
    // });

    // OPEN YOUR WEBCAM
    await navigator.mediaDevices.getUserMedia({
      video: true,
      audio: true,
    }).then(stream => {
      const call = peer.call(codeid, stream);
      videocurrent.srcObject = stream;
      videocurrent.play();
      call.on('stream', renderYouWebcam);
    }).catch(err => console.log('Error: ' + err));
  };

  // On component mount, initialize Peer
  onMount(() => {
    // Add any additional setup code here if needed
  });
</script>

<div>
  You ID cam = {youid} <br>
  Code: <input type="text" bind:value={codeid} name="codeid">
  
  <!-- BUTTON CONNECT TO FRIEND -->
  <button on:click={connectToFriend}>
    Connect
  </button>

  <!-- VIDEO YOUR FRIEND TAG HTML -->
  <video bind:this={videoEl} width="400" height="400" autoplay="true">
    <track kind="captions" src="">
  </video>
  <br>

  <!-- YOUR FACE CAM HERE -->
  <video bind:this={videocurrent} width="400" height="400" autoplay="true">
    <track kind="captions" src="">
  </video>
  
</div>
