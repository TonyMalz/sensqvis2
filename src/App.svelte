<script>
  import Button, { Group } from "@smui/button";
  import { fly, fade, slide } from "svelte/transition";
  import TopAppBar, { Row, Section, Title } from "@smui/top-app-bar";
  import { Label, Icon } from "@smui/common";
  import Textfield from "@smui/textfield";
  import HelperText from "@smui/textfield/helper-text";
  import Tab from "@smui/tab";
  import TabBar from "@smui/tab-bar";
  import IconButton from "@smui/icon-button";
  import Drawer, {
    AppContent,
    Content,
    Header,
    Subtitle,
    Scrim
  } from "@smui/drawer";
  import H6 from "@smui/common/H6.svelte";

  import List, {
    Item,
    Text,
    Graphic,
    Separator,
    Subheader,
    PrimaryText,
    SecondaryText,
    Meta
  } from "@smui/list";

  import Card, {
    PrimaryAction,
    Actions,
    ActionButtons,
    Media,
    MediaContent,
    ActionIcons
  } from "@smui/card";

  import { tasks } from "./modules/db";
  import Slider from "@smui/slider";

  let superText = "";

  // tabs

  let iconTabs = [
    {
      icon: "access_time",
      label: "Recents"
    },
    {
      icon: "near_me",
      label: "Nearby"
    },
    {
      icon: "favorite",
      label: "Favorites"
    }
  ];

  const menuItems = [
    {
      icon: "folder",
      label: "My Studies"
    },
    {
      icon: "save_alt",
      label: "Export"
    },
    {
      icon: "build",
      label: "Preferences"
    }
  ];

  const studyViews = [
    {
      icon: "folder",
      label: "Overview"
    },
    {
      icon: "save_alt",
      label: "Descriptives"
    },
    {
      icon: "build",
      label: "User view"
    },
    {
      icon: "build",
      label: "Custom view"
    }
  ];
  let clicked = studyViews[0].label;

  const prioIcons = ["", "error_outline", "warning", "battery_alert"];

  const tabs = [
    { label: "Study 1", icon: "folder_open" },
    { label: "Study 2", icon: "folder_open" },
    { label: "Study 3", icon: "folder_open" },
    { label: "Study 4", icon: "folder_open" }
  ];
  let active = tabs[0];
  // tabs

  // drawer
  let myDrawerOpen = false;
  let active2 = "Tasks";
  function setActive2(value) {
    active2 = value;
    myDrawerOpen = false;
  }

  function doAction() {}
  let slider = 0;
  // drawer
</script>

<style>
  /* .grayed {
    opacity: 0.6;
  }
  section > div {
    margin-bottom: 40px;
  } */

  /* .icon-indicators
    :global(.mdc-tab-indicator--active .mdc-tab-indicator__content) {
    opacity: 0.2;
  } */
  .cards :global(.mdc-card) {
    margin: 20px;
  }

  .drawer-container {
    position: relative;
    display: flex;
    height: 81vh;
    /* max-width: 600px; */
    border: 1px solid rgba(0, 0, 0, 0.1);
    overflow: auto;
    z-index: 0;
  }
</style>

<TopAppBar variant="static">
  <Row>
    <Section>
      <IconButton
        class="material-icons"
        on:click={() => (myDrawerOpen = !myDrawerOpen)}>
        menu
      </IconButton>
      <Title>SensQVis</Title>
    </Section>
    <Section align="end" toolbar>
      <IconButton class="material-icons" aria-label="User">
        person_outline
      </IconButton>
    </Section>
  </Row>
</TopAppBar>
<Drawer variant="modal" bind:open={myDrawerOpen}>
  <Content>
    <List>
      <Subheader>Menu</Subheader>
      {#each menuItems as item}
        <Item
          href="javascript:void(0)"
          on:click={() => setActive2('Tasks')}
          activated={active2 === item.label}>
          <Graphic class="material-icons" aria-hidden="true">
            {item.icon}
          </Graphic>
          <Text>{item.label}</Text>
        </Item>
      {/each}
      <Separator nav />
      <Subheader>Recent Studies</Subheader>
      <Item
        href="javascript:void(0)"
        on:click={() => setActive2('Family')}
        activated={active2 === 'Family'}>
        <Graphic class="material-icons" aria-hidden="true">bookmark</Graphic>
        <Text>Study 2</Text>
      </Item>
      <Item
        href="javascript:void(0)"
        on:click={() => setActive2('Friends')}
        activated={active2 === 'Friends'}>
        <Graphic class="material-icons" aria-hidden="true">bookmark</Graphic>
        <Text>Study 1</Text>
      </Item>
      <Item
        href="javascript:void(0)"
        on:click={() => setActive2('Work')}
        activated={active2 === 'Work'}>
        <Graphic class="material-icons" aria-hidden="true">bookmark</Graphic>
        <Text>Study 3</Text>
      </Item>
    </List>
  </Content>
</Drawer>
<Scrim />
<AppContent>
  <TabBar {tabs} let:tab bind:active>
    <Tab {tab} minWidth>
      <Icon class="material-icons">{tab.icon}</Icon>
      <Label>{tab.label}</Label>
    </Tab>
  </TabBar>

  <div class="drawer-container">
    <Drawer>
      <Content>
        <List>
          <Subheader>Views</Subheader>
          {#each studyViews as view}
            <Item
              href="javascript:void(0)"
              on:click={() => (clicked = view.label)}
              activated={clicked === view.label}>
              <Text>{view.label}</Text>
            </Item>
          {/each}
        </List>
      </Content>
    </Drawer>

    <AppContent class="app-content">
      <div class="cards">
        <Card padded>
          <Actions>
            <ActionIcons>
              <IconButton
                on:click={() => clicked++}
                toggle
                aria-label="Add to favorites"
                title="Add to favorites">
                <Icon class="material-icons" on>favorite</Icon>
                <Icon class="material-icons">favorite_border</Icon>
              </IconButton>
              <IconButton
                class="material-icons"
                on:click={() => clicked++}
                title="Share">
                share
              </IconButton>
              <IconButton
                class="material-icons"
                on:click={() => clicked++}
                title="More options">
                more_vert
              </IconButton>
            </ActionIcons>
          </Actions>
          <Content>
            <PrimaryText>User 123</PrimaryText>
            <SecondaryText>
              Availability {slider}
              <div>
                <Slider bind:value={slider} min={-10} max={10} discrete />
              </div>
            </SecondaryText>
          </Content>
          <Actions>
            <ActionButtons>
              <Button variant="raised" on:click={() => doAction('addToCart')}>
                <Label>Export</Label>
              </Button>
              <Button dense="true" on:click={() => doAction('buyNow')}>
                <Label>remove</Label>
              </Button>
            </ActionButtons>
          </Actions>
        </Card>
        <Card padded>
          <PrimaryAction on:click={() => clicked++}>
            <Media class="card-media-16x9" aspectRatio="16x9">
              <MediaContent>
                <div
                  style="color: #fff; position: absolute; bottom: 16px; left:
                  16px;">
                  <h2 class="mdc-typography--headline6" style="margin: 0;">
                    A card with media.
                  </h2>
                  <h3 class="mdc-typography--subtitle2" style="margin: 0;">
                    And a subtitle.
                  </h3>
                </div>
              </MediaContent>
            </Media>
            <Content class="mdc-typography--body2">
              It's all in this card. It's a veritable smorgasbord of card
              features.
            </Content>
          </PrimaryAction>
          <Actions>
            <ActionButtons>
              <Button on:click={() => clicked++}>
                <Label>Action</Label>
              </Button>
              <Button on:click={() => clicked++}>
                <Label>Another</Label>
              </Button>
            </ActionButtons>
            <ActionIcons>
              <IconButton
                on:click={() => clicked++}
                toggle
                aria-label="Add to favorites"
                title="Add to favorites">
                <Icon class="material-icons" on>favorite</Icon>
                <Icon class="material-icons">favorite_border</Icon>
              </IconButton>
              <IconButton
                class="material-icons"
                on:click={() => clicked++}
                title="Share">
                share
              </IconButton>
              <IconButton
                class="material-icons"
                on:click={() => clicked++}
                title="More options">
                more_vert
              </IconButton>
            </ActionIcons>
          </Actions>
        </Card>

      </div>

    </AppContent>
  </div>

</AppContent>
