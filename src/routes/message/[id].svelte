<script lang="ts">
  import IonPage from "$ionic/svelte/components/IonPage.svelte";
  import { fly, fade } from "svelte/transition";
  import { getMessageById } from "$services/data";

  import { goto } from "@roxi/routify";
  import { params } from "@roxi/routify";
  import { personCircle, chevronBack } from "ionicons/icons";

  let { id } = $params;
  console.log("asdasdas", id);
  const message = getMessageById(parseInt(id, 10));

  const getBackButtonText = () => {
    const win = window as any;
    const mode = win && win.Ionic && win.Ionic.mode;
    return mode === "ios" ? "Inbox" : "";
  };
</script>

<ion-header translucent="true">
  <ion-toolbar>
    <ion-buttons
      slot="start"
      on:click={() => {
        $goto("/home");
      }}
    >
      <ion-icon icon={chevronBack} /> Back
    </ion-buttons>
  </ion-toolbar>
</ion-header>

<ion-content fullscreen="true">
  <ion-item>
    <ion-icon icon={personCircle} color="primary" />
    <ion-label class="ion-text-wrap">
      <h2>
        {message.fromName}
        <span class="date">
          <ion-note>{message.date}</ion-note>
        </span>
      </h2>
      <h3>To: <ion-note>Me</ion-note></h3>
    </ion-label>
  </ion-item>

  <div class="ion-padding">
    <h1>{message.subject}</h1>
    <p>
      Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut
      labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco
      laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in
      voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat
      non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
    </p>
  </div>
</ion-content>

<style>
  ion-item {
    --inner-padding-end: 0;
    --background: transparent;
  }

  ion-label {
    margin-top: 12px;
    margin-bottom: 12px;
  }

  ion-item h2 {
    font-weight: 600;
  }

  ion-item .date {
    float: right;
    align-items: center;
    display: flex;
  }

  ion-item ion-icon {
    font-size: 42px;
    margin-right: 8px;
  }

  ion-item ion-note {
    font-size: 15px;
    margin-right: 12px;
    font-weight: normal;
  }

  h1 {
    margin: 0;
    font-weight: bold;
    font-size: 22px;
  }

  p {
    line-height: 22px;
  }
</style>
