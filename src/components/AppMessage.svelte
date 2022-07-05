<script lang="ts">
  import { goto, url } from "@roxi/routify";
  import { chevronForward } from "ionicons/icons";

  export let message;

  const isIos = () => {
    const win = window as any;
    return win && win.Ionic && win.Ionic.mode === "ios";
  };

  const gotoLink = (id) => {
    console.log("Link", id);
    $goto("/message/[id]", { id });
  };

  /*
on:click={() => {
    gotoLink(message.id);
  }}


  */
</script>

<ion-item
  button
  detail="false"
  on:click={() => {
    gotoLink(message.id);
  }}
>
  <div slot="start" class="dot" class:dot-unread={!message.read} />
  <ion-label class="ion-text-wrap">
    <h2>
      {message.fromName}
      <span class="date">
        <ion-note>{message.date}</ion-note>
        {#if isIos()}
          <ion-icon icon={chevronForward} size="small" />
        {/if}
      </span>
    </h2>
    <h3>{message.subject}</h3>
    <p>
      Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut
      labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco
      laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in
      voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat
      non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
    </p>
  </ion-label>
</ion-item>

<style>
  ion-item {
    --padding-start: 0;
    --inner-padding-end: 0;
  }

  ion-label {
    margin-top: 12px;
    margin-bottom: 12px;
  }

  ion-item h2 {
    font-weight: 600;
    margin: 0;
  }

  ion-item p {
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
    width: 95%;
  }

  ion-item .date {
    float: right;
    align-items: center;
    display: flex;
  }

  ion-item ion-icon {
    color: #c9c9ca;
  }

  ion-item ion-note {
    font-size: 15px;
    margin-right: 8px;
    font-weight: normal;
  }

  ion-item ion-note.md {
    margin-right: 14px;
  }

  .dot {
    display: block;
    height: 12px;
    width: 12px;
    border-radius: 50%;
    align-self: start;
    margin: 16px 10px 16px 16px;
  }

  .dot-unread {
    background: var(--ion-color-primary);
  }

  ion-footer ion-title {
    font-size: 11px;
    font-weight: normal;
  }
</style>
