# Component Composition (Dumb components ftw)
Instead of doing:

```javascript
<Dashboard />
```

you would break it up to be:
```javascript
<Dashboard>
  <DashboardHeader />
  <UserAnalytics />
  <Summery />
</Dashboard>
```


## Example:


### Example 1

```javascript
<Dialog
  title={title}
  open={isOpen}
  onClose={onClose}
  thirdButtonText={actions.secondary?.text}
  thirdButtonAction={() => handleAction(actions.secondary?.type)}
  hideThirdButton={!actions.secondary}
  thirdButtonStyle={dialogStyles.cancelButton}
  onSubmit={() => handleAction(actions.primary?.type)}
  submitButtonText={actions.primary?.text}
  hideSubmit={!actions.primary}
  disableSubmit={false}>
  Content
</Dialog>
```

After:
```javascript
<Dialog
  title={title}
  open={isOpen}
  onClose={onClose}
>
  Content
  <Dialog.Footer>
    {actions.customerService && (
      <Link to={..} target="_blank">...</Link>
    )}
    {actions.secondary && (
      <Button buttonType="cancel" onClick={...} >
        ...
      </Button>
    )}
    {actions.primary && (
      <Button onClick={..}>
        {actions.primary?.text}
      </Button>
    )}
  </Dialog.Footer>
</Dialog>
```


### Example 2

Before:
```javascript

<FilterBarModule
  key={filterModuleTimestamp}
  controller={(filters, page) =>
    ClaimHistoryController.getClaimHistoryResults(filters, page)
  }
  filters={filters}
  preselectedFilters={filtersObject.filters}
  observe={{
    page: filtersObject.pagination.page
  }}
  onFilterChange={filters => handleFiltersChange(filters)}
  visibleFiltersCount={9}
  withSettings
  expandableDialogSubtitle={strings.CUSTOMER_SERVICE_FILTERS_NOTIFICATION}
  expandable
  appendPaginationRecords
  autoReload
  autoReloadFiltersOverride={autoReloadFiltersOverride}
/>
<SortableTableModule
  items={this.getTableRows()}
  headers={this.getTableHeaders()}
  hasPagination
  pagination={filtersObject.pagination}
  selectPage={page => this.selectPage(page)}
/>
```

After:
```javascript
const [filters, setFilters] = useState({})
const [page, setPage] = useState(0)

useEffect(() => {},
  getItems(filters, page)
[filters, page])

<Filters
  onChange={setFilters}
/>
<Filters filterOptions={getFilters()} filters={filters} onChange={setFilters} >

<Table sections={items} />

<LoadMore
  disabled={page + 1 === totalPages || !totalPages}
  handleLoadMore={}
  buttonClass={styles.loadMorePricing}
/>
```
