<template>
<article class="page">
  <header>
    <h1>Toolbar <code>&lt;pf-toolbar&gt;</code></h1>
  </header>

  <section>
    <p>This component implements a toolbar with controls for filters, sorting, searching and custom actions to interact with a data view.</p>

    <h4>Related documentation</h4>
    <ol>
      <li><a href="http://www.patternfly.org/pattern-library/forms-and-controls/toolbar/#_" target="_blank">Pattern Library > Toolbar</a></li>
    </ol>

    <pf-toolbar ref="toolbar"
                :view="toolbar.view"
                :views="toolbar.views"
                @view="toolbar.view = arguments[0]"
                @columns="toolbar.pickedColumns = arguments[0]"
                @filters="toolbar.filters = arguments[0]"
                :filters="toolbar.filters"
                :filter-fields="toolbar.filterFields"
                @sort-by="setSort"
                :sort-by="toolbar.sortBy"
                :sort-direction="toolbar.sortDirection"
                :sort-fields="toolbar.sortFields"
                :result-count="toolbar.resultCount"
                :attached="toolbar.attached"
                :columns="toolbar.columns"
                :picked-columns="toolbar.pickedColumns">

      <div v-if="toolbar.slotDefault" v-html="toolbar.slotDefault" style="float:left"></div>

      <bs-dropdown class="dropdown-kebab-pf" type="link">
        <li role="menuitem">
          <a title="Menu Title 1">Menu Item 1</a>
        </li>
        <li role="menuitem">
          <a title="Menu Title 2">Menu Item 2</a>
        </li>
        <li role="separator" class="divider"></li>
        <li role="menuitem">
          <a title="Menu Title 3">Menu Item 3</a>
        </li>
      </bs-dropdown>
    </pf-toolbar>

    <props-table :component-props="toolbarProps">
      <props-row name="attached" description="Use the layout for the toolbar attached to an adjacient table" v-model="toolbar.attached"></props-row>
      <props-row name="filterFields" description="List of available fields for filtering" v-model="toolbar.filterFields" code></props-row>
      <props-row name="filters" description="List of active filters" v-model="toolbar.filters" code></props-row>
      <props-row name="view" description="Active view" v-model="toolbar.view"></props-row>
      <props-row name="views" description="List of available views (names separated by comma)" v-model="toolbar.views"></props-row>
      <props-row name="sortBy" description="Selected sorting field" v-model="toolbar.sortBy"></props-row>
      <props-row name="sortDirection" description="Selected sorting direction" v-model="toolbar.sortDirection" :options="['ascending', 'descending']"></props-row>
      <props-row name="sortFields" description="List of available fields for sorting" v-model="toolbar.sortFields" code></props-row>
      <props-row name="columns" description="List of available columns to display" v-model="toolbar.columns" code></props-row>
      <props-row name="pickedColumns" description="List of available columns to display" v-model="toolbar.pickedColumns" code></props-row>
      <props-row name="resultCount" description="Number of elements matching the filter criteria" v-model="toolbar.resultCount"></props-row>
    </props-table>

    <slots-table>
      <slots-row name="default" description="Action buttons and dropdowns can be placed here" v-model="toolbar.slotDefault"></slots-row>
    </slots-table>
  </section>
</article>
</template>

<script>
import VuePatternfly from 'vue-patternfly';

export default {
  name: 'cards-page',

  data() {
    return {
      toolbarProps: VuePatternfly.Toolbar.props,
      toolbar: {
        view: 'table',
        views: 'table,card,list',
        filters: [],
        filterFields: {
          name: {
            label: 'Name',
          },
          age: {
            label: 'Age',
          },
          address: {
            label: 'Address',
          },
          birthMonth: {
            label: 'Birth Month',
            placeholder: 'Filter by Birth Month...',
            values: ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'],
          }
        },
        sortBy: 'date',
        sortDirection: 'ascending',
        sortFields: {
          name: 'Name',
          date: 'Date',
          age: {
            label: 'Age',
            type: 'numeric',
          },
        },
        columns: ['Name', 'Date'],
        pickedColumns: ['Name'],
        resultCount: 0,
        attached: false,
        slotDefault: `<button class="btn btn-default" type="button" title="Title 1">
  Action 1
</button>
<button class="btn btn-default" type="button" title="Title 2">
  Action 2
</button>
<button class="btn btn-danger" type="button" title="Title 3">
  Action 3
</button>

<!-- The "kebab" menu is fixed in this example due to how v-html works -->`,
      },
    };
  },

  methods: {
    setSort(field, direction) {
      this.toolbar.sortBy = field;
      this.toolbar.sortDirection = direction;
    },
    addFilter(filter, value) {
      const f = {};
      f[filter.title] = value;
      this.toolbar.filters.push(f);
    },
  },
};
</script>
