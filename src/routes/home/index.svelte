<script lang="ts">
  import AppMessage from "$components/AppMessage.svelte";
  import IonPage from "$lib/ionic/svelte/components/IonPage.svelte";
  import { getMessages as getMessagesFromService } from "$services/data";
  import { goto, url } from "@roxi/routify";

  console.log("sadads", $url("/message/[id]", { id: "5" }));

  // $goto($url("/message/[id]", { id: "5" }));
  const refresh = (event) => {
    setTimeout(() => {
      event.detail.complete();
    }, 3000);
  };

  const getMessages = () => {
    return getMessagesFromService();
  };
</script>

<ion-header translucent="true">
  <ion-toolbar>
    <ion-title> Inbox </ion-title>
  </ion-toolbar>
</ion-header>

<ion-content fullscreen="true">
  <ion-refresher slot="fixed" on:ionRefresh={refresh}>
    <ion-refresher-content />
  </ion-refresher>

  <ion-header collapse="condense">
    <ion-toolbar>
      <ion-title size="large"> Inbox </ion-title>
    </ion-toolbar>
  </ion-header>

  <ion-list>
    {#each getMessages() as message}
      <AppMessage {message} />
    {/each}
  </ion-list>
</ion-content>
