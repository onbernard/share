
<script>
    import DataTable, {
      Head,
      Body,
      Row,
      Cell,
      Label,
      SortValue,
    } from '@smui/data-table';
    import IconButton from '@smui/icon-button';
    import items from './call.json'
    let sort = 'id';
    let sortDirection = 'ascending';
    function handleSort() {
      items.sort((a, b) => {
        const [aVal, bVal] = [a[sort], b[sort]][
          sortDirection === 'ascending' ? 'slice' : 'reverse'
        ]();
        if (typeof aVal === 'string' && typeof bVal === 'string') {
          return aVal.localeCompare(bVal);
        }
        return Number(aVal) - Number(bVal);
      });
      items = items;
    }
  </script>

<DataTable
  sortable
  bind:sort
  bind:sortDirection
  on:SMUIDataTable:sorted={handleSort}
  table$aria-label="User list"
  style="width: 100%;"
  stickyHeader
>
  <Head>
    <Row>
      <!--
        Note: whatever you supply to "columnId" is
        appended with "-status-label" and used as an ID
        for the hidden label that describes the sort
        status to screen readers.
        You can localize those labels with the
        "sortAscendingAriaLabel" and
        "sortDescendingAriaLabel" props on the DataTable.
      -->
      <Cell numeric columnId="id">
        <!-- For numeric columns, icon comes first. -->
        <IconButton class="material-icons">arrow_upward</IconButton>
        <Label>ID</Label>
      </Cell>
      <Cell columnId="device" style="width: 100%;">
        <Label>Device</Label>
        <!-- For non-numeric columns, icon comes second. -->
        <IconButton class="material-icons">arrow_upward</IconButton>
      </Cell>
      <Cell columnId="direction">
        <Label>Direction</Label>
        <IconButton class="material-icons">arrow_upward</IconButton>
      </Cell>
      <Cell columnId="status">
        <Label>Status</Label>
        <IconButton class="material-icons">arrow_upward</IconButton>
      </Cell>
      <!-- You can turn off sorting for a column. -->
      <Cell sortable={false}>Duration</Cell>
    </Row>
  </Head>
  <Body>
    {#each items as item (item.id)}
      <Row>
        <Cell numeric>{item.id}</Cell>
        <Cell>{item.device}</Cell>
        <Cell>{item.direction}</Cell>
        <Cell>{item.status}</Cell>
        <Cell>{item.duration}</Cell>
      </Row>
    {/each}
  </Body>
</DataTable>
