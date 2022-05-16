<script>
  /*imports*/
  import {
    NavigationDrawer,
    List,
    ListItem,
    Subheader,
    Button,
    Icon,
    MaterialApp,
    Container,
  } from "svelte-materialify";
  import {
    mdiViewDashboard,
    mdiAccountBox,
    mdiGavel,
    mdiTagSearchOutline,
    mdiTestTube,
    mdiDatabaseSync,
  } from "@mdi/js";

  import Counter from "$lib/Counter.svelte";
  import AuditSql from "$lib/AuditSql.svelte";
  import Teste from "$lib/Teste.svelte";
  import Microservicos from "$lib/Microservicos.svelte";

  /**definições*/
  
  let page = [];
  let components = [
    { name: "microserv", component: Microservicos },
    { name: "audit", component: AuditSql },
    { name: "teste", component: Teste },
  ];

  /**functions*/

  const handleComponentClick = (item) => {
    page = item != null ? components.find((x) => x.name === item) : [];
  };
  
</script>

<MaterialApp>
  <div class="d-flex left">
    <NavigationDrawer style="height:653px" class="primary-color theme--dark">
      <List>
        <Subheader><h5>Devops App</h5></Subheader>
        <ListItem
          on:click={() => {
            handleComponentClick("audit");
          }}
        >
          <span slot="prepend">
            <Icon path={mdiTagSearchOutline} />
          </span>
          Auditoria
        </ListItem>
        <ListItem
          on:click={() => {
            handleComponentClick("microserv");
          }}
        >
          <span slot="prepend">
            <Icon path={mdiDatabaseSync} />
          </span>
          Micro Serviços
        </ListItem>
        <ListItem
          on:click={() => {
            handleComponentClick("teste");
          }}
        >
          <span slot="prepend">
            <Icon path={mdiTestTube} />
          </span>
          Teste Diversos
        </ListItem>
      </List>
      <span slot="append" class="pa-2">
        <Button block>Logout</Button>
      </span>
    </NavigationDrawer>
    <Container>
      <svelte:component this={page.component} />
    </Container>
  </div>
</MaterialApp>
