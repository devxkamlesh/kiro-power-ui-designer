# Dashboard Design Workflow

## When to Use This Workflow

Activate when user:
- Designs analytics dashboards
- Creates data visualization interfaces
- Plans KPI displays
- Implements admin dashboards
- Designs reporting interfaces
- Creates monitoring dashboards

---

## Production-Grade Dashboard Design

### Phase 1: Dashboard Architecture

**Dashboard Layout Pattern:**

```
┌─────────────────────────────────────────────────────────┐
│ Dashboard Header                                        │
│ [Title] [Date Range] [Export] [Refresh]                │
├─────────────────────────────────────────────────────────┤
│                                                         │
│ KPI Cards Row                                           │
│ ┌──────┐ ┌──────┐ ┌──────┐ ┌──────┐                   │
│ │ KPI1 │ │ KPI2 │ │ KPI3 │ │ KPI4 │                   │
│ └──────┘ └──────┘ └──────┘ └──────┘                   │
│                                                         │
│ Charts Section                                          │
│ ┌─────────────────┐ ┌─────────────────┐               │
│ │ Line Chart      │ │ Bar Chart       │               │
│ │                 │ │                 │               │
│ └─────────────────┘ └─────────────────┘               │
│                                                         │
│ Data Table                                              │
│ ┌─────────────────────────────────────────────────┐   │
│ │ [Filters] [Search] [Columns]                    │   │
│ │ ┌───────────────────────────────────────────┐   │   │
│ │ │ Table with sortable columns               │   │   │
│ │ └───────────────────────────────────────────┘   │   │
│ └─────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
```

---

### Phase 2: KPI Card Design

**Effective KPI Cards:**

```tsx
<KPICard>
  <KPIHeader>
    <KPIIcon>
      <TrendingUp />
    </KPIIcon>
    <KPITitle>Total Revenue</KPITitle>
    <KPITooltip>
      <InfoIcon />
      <TooltipContent>
        Total revenue from all sources this month
      </TooltipContent>
    </KPITooltip>
  </KPIHeader>

  <KPIValue>
    <ValueAmount>$124,563</ValueAmount>
    <ValueChange positive>
      <ArrowUp />
      <ChangePercent>+12.5%</ChangePercent>
      <ChangeLabel>vs last month</ChangeLabel>
    </ValueChange>
  </KPIValue>

  <KPISparkline>
    <MiniChart data={revenueData} type="line" />
  </KPISparkline>

  <KPIFooter>
    <FooterLink href="/reports/revenue">
      View Details →
    </FooterLink>
  </KPIFooter>
</KPICard>
```

**KPI Design Rules:**

```
✅ DO:
- Show trend direction (↑↓)
- Use color for meaning (green=good, red=bad)
- Include comparison period
- Add sparklines for context
- Keep numbers scannable
- Use consistent formatting

❌ DON'T:
- Overload with data
- Use ambiguous colors
- Hide units ($, %, etc.)
- Make clickable without indication
- Use tiny fonts
```

---

### Phase 3: Chart Selection Guide

**Chart Type Decision Matrix:**

| Data Type | Best Chart | Use Case |
|-----------|------------|----------|
| Trends over time | Line Chart | Revenue, users, traffic |
| Comparisons | Bar Chart | Sales by region, product comparison |
| Parts of whole | Pie/Donut | Market share, category breakdown |
| Relationships | Scatter Plot | Correlation, clustering |
| Distribution | Histogram | Age groups, price ranges |
| Hierarchical | Treemap | File sizes, budget allocation |
| Geographic | Map | Regional data, locations |

**Chart Implementation:**

```tsx
<ChartCard>
  <ChartHeader>
    <ChartTitle>Revenue Trend</ChartTitle>
    <ChartActions>
      <ChartTypeSelector
        value={chartType}
        onChange={setChartType}
        options={['line', 'bar', 'area']}
      />
      <ExportButton onClick={exportChart}>
        <Download /> Export
      </ExportButton>
    </ChartActions>
  </ChartHeader>

  <ChartContainer>
    <ResponsiveContainer width="100%" height={300}>
      <LineChart data={data}>
        <CartesianGrid strokeDasharray="3 3" />
        <XAxis 
          dataKey="date" 
          tickFormatter={formatDate}
        />
        <YAxis 
          tickFormatter={formatCurrency}
        />
        <Tooltip 
          content={<CustomTooltip />}
        />
        <Legend />
        <Line 
          type="monotone" 
          dataKey="revenue" 
          stroke="#3B82F6"
          strokeWidth={2}
          dot={{ r: 4 }}
          activeDot={{ r: 6 }}
        />
      </LineChart>
    </ResponsiveContainer>
  </ChartContainer>

  <ChartFooter>
    <ChartLegend>
      <LegendItem color="#3B82F6">Revenue</LegendItem>
      <LegendItem color="#10B981">Target</LegendItem>
    </ChartLegend>
  </ChartFooter>
</ChartCard>
```

---

### Phase 4: Data Table Design

**Advanced Data Table:**

```tsx
<DataTableCard>
  <TableHeader>
    <TableTitle>Recent Transactions</TableTitle>
    <TableActions>
      <SearchInput
        placeholder="Search transactions..."
        value={search}
        onChange={setSearch}
      />
      <FilterButton onClick={openFilters}>
        <Filter /> Filters {activeFilters > 0 && `(${activeFilters})`}
      </FilterButton>
      <ColumnSelector
        columns={columns}
        visible={visibleColumns}
        onChange={setVisibleColumns}
      />
      <ExportButton onClick={exportData}>
        <Download /> Export
      </ExportButton>
    </TableActions>
  </TableHeader>

  <TableContainer>
    <Table>
      <TableHead>
        <TableRow>
          <TableHeadCell sortable onSort={() => handleSort('id')}>
            ID
            {sortColumn === 'id' && (
              sortDirection === 'asc' ? <ArrowUp /> : <ArrowDown />
            )}
          </TableHeadCell>
          <TableHeadCell sortable onSort={() => handleSort('date')}>
            Date
          </TableHeadCell>
          <TableHeadCell sortable onSort={() => handleSort('amount')}>
            Amount
          </TableHeadCell>
          <TableHeadCell>Status</TableHeadCell>
          <TableHeadCell>Customer</TableHeadCell>
          <TableHeadCell>Actions</TableHeadCell>
        </TableRow>
      </TableHead>
      <TableBody>
        {data.map((row) => (
          <TableRow key={row.id} onClick={() => viewDetails(row.id)}>
            <TableCell>
              <CellContent>
                <MonoText>#{row.id}</MonoText>
              </CellContent>
            </TableCell>
            <TableCell>
              <CellContent>
                <DateText>{formatDate(row.date)}</DateText>
                <TimeText>{formatTime(row.date)}</TimeText>
              </CellContent>
            </TableCell>
            <TableCell>
              <CellContent>
                <AmountText>{formatCurrency(row.amount)}</AmountText>
              </CellContent>
            </TableCell>
            <TableCell>
              <StatusBadge status={row.status}>
                {row.status}
              </StatusBadge>
            </TableCell>
            <TableCell>
              <CellContent>
                <CustomerInfo>
                  <Avatar src={row.customer.avatar} size="sm" />
                  <CustomerName>{row.customer.name}</CustomerName>
                </CustomerInfo>
              </CellContent>
            </TableCell>
            <TableCell>
              <TableActions>
                <ActionButton icon={Eye} onClick={() => view(row.id)}>
                  View
                </ActionButton>
                <ActionButton icon={Edit} onClick={() => edit(row.id)}>
                  Edit
                </ActionButton>
              </TableActions>
            </TableCell>
          </TableRow>
        ))}
      </TableBody>
    </Table>
  </TableContainer>

  <TableFooter>
    <TableInfo>
      Showing {startRow}-{endRow} of {totalRows} transactions
    </TableInfo>
    <Pagination
      currentPage={page}
      totalPages={totalPages}
      onPageChange={setPage}
    />
  </TableFooter>
</DataTableCard>
```

**Table Performance:**

```typescript
// Virtualize large tables (>100 rows)
import { useVirtualizer } from '@tanstack/react-virtual';

function VirtualizedTable({ data }) {
  const parentRef = useRef<HTMLDivElement>(null);

  const virtualizer = useVirtualizer({
    count: data.length,
    getScrollElement: () => parentRef.current,
    estimateSize: () => 50, // Row height
    overscan: 10,
  });

  return (
    <TableContainer ref={parentRef} style={{ height: '600px' }}>
      <Table style={{ height: `${virtualizer.getTotalSize()}px` }}>
        <TableBody>
          {virtualizer.getVirtualItems().map((virtualRow) => {
            const row = data[virtualRow.index];
            return (
              <TableRow
                key={row.id}
                style={{
                  position: 'absolute',
                  top: 0,
                  left: 0,
                  width: '100%',
                  height: `${virtualRow.size}px`,
                  transform: `translateY(${virtualRow.start}px)`,
                }}
              >
                {/* Row content */}
              </TableRow>
            );
          })}
        </TableBody>
      </Table>
    </TableContainer>
  );
}
```

---

### Phase 5: Filters & Date Range

**Advanced Filtering:**

```tsx
<FilterPanel>
  <FilterHeader>
    <FilterTitle>Filters</FilterTitle>
    <FilterActions>
      <ClearButton onClick={clearFilters}>
        Clear All
      </ClearButton>
      <CloseButton onClick={closeFilters}>
        <X />
      </CloseButton>
    </FilterActions>
  </FilterHeader>

  <FilterContent>
    <FilterSection>
      <FilterLabel>Date Range</FilterLabel>
      <DateRangePicker
        value={dateRange}
        onChange={setDateRange}
        presets={[
          { label: 'Today', value: 'today' },
          { label: 'Last 7 days', value: 'last7days' },
          { label: 'Last 30 days', value: 'last30days' },
          { label: 'This month', value: 'thisMonth' },
          { label: 'Last month', value: 'lastMonth' },
          { label: 'Custom', value: 'custom' },
        ]}
      />
    </FilterSection>

    <FilterSection>
      <FilterLabel>Status</FilterLabel>
      <CheckboxGroup value={statusFilter} onChange={setStatusFilter}>
        <Checkbox value="completed">
          Completed <Badge>{counts.completed}</Badge>
        </Checkbox>
        <Checkbox value="pending">
          Pending <Badge>{counts.pending}</Badge>
        </Checkbox>
        <Checkbox value="failed">
          Failed <Badge>{counts.failed}</Badge>
        </Checkbox>
      </CheckboxGroup>
    </FilterSection>

    <FilterSection>
      <FilterLabel>Amount Range</FilterLabel>
      <RangeSlider
        value={amountRange}
        onChange={setAmountRange}
        min={0}
        max={10000}
        step={100}
        formatLabel={formatCurrency}
      />
      <RangeDisplay>
        {formatCurrency(amountRange[0])} - {formatCurrency(amountRange[1])}
      </RangeDisplay>
    </FilterSection>

    <FilterSection>
      <FilterLabel>Category</FilterLabel>
      <Select
        value={categoryFilter}
        onChange={setCategoryFilter}
        multiple
        placeholder="Select categories"
      >
        {categories.map((cat) => (
          <SelectOption key={cat.id} value={cat.id}>
            {cat.name}
          </SelectOption>
        ))}
      </Select>
    </FilterSection>
  </FilterContent>

  <FilterFooter>
    <Button variant="outline" onClick={resetFilters}>
      Reset
    </Button>
    <Button variant="primary" onClick={applyFilters}>
      Apply Filters
    </Button>
  </FilterFooter>
</FilterPanel>
```

---

### Phase 6: Real-Time Updates

**Live Data Updates:**

```tsx
<DashboardCard>
  <CardHeader>
    <CardTitle>Live Metrics</CardTitle>
    <LiveIndicator>
      <PulsingDot />
      <LiveLabel>Live</LiveLabel>
      <LastUpdate>Updated {timeAgo(lastUpdate)}</LastUpdate>
    </LiveIndicator>
  </CardHeader>

  <CardContent>
    {/* Real-time chart */}
    <RealtimeChart
      data={liveData}
      onDataPoint={(point) => {
        // Animate new data point
        animateNewPoint(point);
      }}
    />
  </CardContent>
</DashboardCard>

// WebSocket connection for real-time data
function useRealtimeData(endpoint: string) {
  const [data, setData] = useState([]);

  useEffect(() => {
    const ws = new WebSocket(endpoint);

    ws.onmessage = (event) => {
      const newData = JSON.parse(event.data);
      setData((prev) => [...prev.slice(-99), newData]); // Keep last 100 points
    };

    return () => ws.close();
  }, [endpoint]);

  return data;
}
```

---

### Phase 7: Empty & Loading States

**Empty State:**

```tsx
<EmptyState>
  <EmptyIcon>
    <BarChart3 size={64} />
  </EmptyIcon>
  <EmptyTitle>No data available</EmptyTitle>
  <EmptyDescription>
    There's no data to display for the selected date range.
    Try adjusting your filters or date range.
  </EmptyDescription>
  <EmptyActions>
    <Button variant="outline" onClick={clearFilters}>
      Clear Filters
    </Button>
    <Button variant="primary" onClick={refreshData}>
      Refresh Data
    </Button>
  </EmptyActions>
</EmptyState>
```

**Loading State:**

```tsx
<DashboardSkeleton>
  {/* KPI Cards Skeleton */}
  <SkeletonRow>
    <SkeletonCard />
    <SkeletonCard />
    <SkeletonCard />
    <SkeletonCard />
  </SkeletonRow>

  {/* Charts Skeleton */}
  <SkeletonRow>
    <SkeletonChart height={300} />
    <SkeletonChart height={300} />
  </SkeletonRow>

  {/* Table Skeleton */}
  <SkeletonTable rows={10} columns={6} />
</DashboardSkeleton>
```

---

## Behavioral Psychology for Dashboards

### Information Hierarchy:
- **Most Important**: Top-left (KPIs)
- **Supporting Data**: Center (Charts)
- **Details**: Bottom (Tables)
- **Actions**: Top-right (Export, filters)

### Cognitive Load Management:
- **Progressive Disclosure**: Show summary first, details on demand
- **Chunking**: Group related metrics
- **Consistent Layout**: Same position for similar data
- **Visual Hierarchy**: Size indicates importance

### Scanning Patterns:
- **F-Pattern**: For text-heavy dashboards
- **Z-Pattern**: For action-oriented dashboards
- **Layer Cake**: For multi-section dashboards

---

## Performance Optimization

```typescript
// Lazy load charts
const ChartComponent = lazy(() => import('./Chart'));

// Memoize expensive calculations
const processedData = useMemo(() => {
  return data.map(item => ({
    ...item,
    calculated: expensiveCalculation(item),
  }));
}, [data]);

// Debounce filter changes
const debouncedFilter = useDebouncedCallback(
  (filters) => applyFilters(filters),
  500
);

// Virtual scrolling for large tables
<VirtualTable
  data={data}
  rowHeight={50}
  height={600}
  overscan={10}
/>
```

---

## Production Checklist

- [ ] KPIs show trend direction
- [ ] Charts have proper labels and legends
- [ ] Tables are sortable and filterable
- [ ] Date range selector included
- [ ] Export functionality works
- [ ] Real-time updates (if applicable)
- [ ] Empty states designed
- [ ] Loading states implemented
- [ ] Mobile responsive
- [ ] Performance optimized (virtualization)
- [ ] Accessibility compliant
- [ ] Color blind friendly
- [ ] Print-friendly styles
- [ ] Keyboard navigation
- [ ] Error handling

---

This workflow ensures production-grade dashboard design with clarity, performance, and usability.
