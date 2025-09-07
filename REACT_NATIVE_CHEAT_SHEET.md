# React Native Quick Notes

## FlatList

### Basic Structure

```jsx
<FlatList
  data={dataArray}
  renderItem={({ item }) => <Component item={item} />}
  keyExtractor={(item) => item.id.toString()}
/>
```

### Most Used Props

```jsx
// Layout
numColumns={2}                    // Grid layout
horizontal={true}                 // Horizontal scroll
columnWrapperClassName="flex gap-5 px-5"  // Column styling
contentContainerClassName="pb-32" // Container styling

// Scroll
showsVerticalScrollIndicator={false}
showsHorizontalScrollIndicator={false}
bounces={false}

// Components
ListHeaderComponent={<Header />}
ListFooterComponent={<Footer />}
ListEmptyComponent={<EmptyState />}

// Events
onEndReached={() => loadMore()}
onEndReachedThreshold={0.5}
onRefresh={() => refresh()}
refreshing={isRefreshing}
```

### Your Project Examples

```jsx
// Grid (2 columns)
<FlatList
  data={[1, 2]}
  renderItem={({ item }) => <Card />}
  numColumns={2}
  columnWrapperClassName="flex gap-5 px-5"
  keyExtractor={(item) => item.toString()}
/>

// Horizontal
<FlatList
  data={[1, 2, 3]}
  renderItem={({ item }) => <FeaturedCard />}
  horizontal
  showsHorizontalScrollIndicator={false}
  keyExtractor={(item) => item.toString()}
/>
```

---

## Common Components

```jsx
// Basic
<View className="flex-1 bg-white">
<Text className="text-lg font-bold">
<Image source={require('./img.png')} className="w-20 h-20" />
<TouchableOpacity onPress={() => {}}>
<TextInput value={text} onChangeText={setText} />
<SafeAreaView className="flex-1">
```

---

## Navigation (Expo Router)

```jsx
// Link
<Link href="/profile" asChild>
  <TouchableOpacity><Text>Go to Profile</Text></TouchableOpacity>
</Link>

// Programmatic
router.push('/profile');
router.push('/profile?id=123');

// Params
const params = useLocalSearchParams<{ id: string }>();
router.setParams({ query: 'search' });
```

---

## NativeWind Classes

```jsx
// Layout
flex - 1, flex - row, flex - col, justify - center, items - center;

// Spacing
p - 4, px - 5, py - 2, m - 3, mt - 5;

// Colors
bg - white, text - black, border - gray - 300;

// Sizing
w - full, h - 20, size - 12;

// Border
rounded - lg, rounded - full;

// Fonts (your project)
font - rubik, font - rubik - bold, font - rubik - medium;
text - primary - 300, bg - accent - 100;
```

---

## State & Hooks

```jsx
// useState
const [count, setCount] = useState(0);
const [user, setUser] = useState({ name: "", email: "" });

// useEffect
useEffect(() => {
  fetchData();
}, []);
useEffect(() => {
  searchData(query);
}, [query]);

// Custom (your project)
const debouncedSearch = useDebouncedCallback((text) => {
  router.setParams({ query: text });
}, 500);
```

---

## Common Patterns

```jsx
// Search & Filter
const [filteredData, setFilteredData] = useState(data);
useEffect(() => {
  const filtered = data.filter((item) =>
    item.title.toLowerCase().includes(searchQuery.toLowerCase())
  );
  setFilteredData(filtered);
}, [searchQuery]);

// Pull to Refresh
const [refreshing, setRefreshing] = useState(false);
const onRefresh = async () => {
  setRefreshing(true);
  await fetchData();
  setRefreshing(false);
};

// Loading States
{
  loading ? <ActivityIndicator /> : <FlatList data={data} />;
}

// Conditional Rendering
{
  user ? <ProfileScreen /> : <LoginScreen />;
}
{
  items.length > 0 && <FlatList data={items} />;
}
```
