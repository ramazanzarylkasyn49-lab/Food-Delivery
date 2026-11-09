import React, { useState, useEffect, useRef } from 'react';
import {
  View,
  Text,
  TextInput,
  TouchableOpacity,
  StyleSheet,
  SafeAreaView,
  ScrollView,
  KeyboardAvoidingView,
  Platform,
  Alert,
} from 'react-native';
import { StatusBar } from 'expo-status-bar';

const ORANGE = '#FF8A00';
const DARK = '#1F1F2E';
const LIGHT_ORANGE = '#FFF1E0';
const GRAY_BG = '#F0F2F7';

function Header({ title, onBack }) {
  return (
    <View style={styles.header}>
      {onBack ? (
        <TouchableOpacity onPress={onBack}>
          <Text style={styles.back}>‹</Text>
        </TouchableOpacity>
      ) : null}
      <Text style={styles.headerTitle}>{title}</Text>
    </View>
  );
}

function Illustration({ emoji }) {
  return (
    <View style={styles.illustrationWrap}>
      <View style={styles.circle}>
        <Text style={{ fontSize: 56 }}>{emoji}</Text>
      </View>
    </View>
  );
}

function Input(props) {
  return (
    <TextInput
      style={styles.input}
      placeholderTextColor="#B0B0B0"
      {...props}
    />
  );
}

function Button({ title, onPress, disabled }) {
  return (
    <TouchableOpacity
      style={[styles.button, disabled && styles.buttonDisabled]}
      onPress={onPress}
      disabled={disabled}
    >
      <Text style={styles.buttonText}>{title}</Text>
    </TouchableOpacity>
  );
}

function RoundBtn({ children, onPress, dark }) {
  return (
    <TouchableOpacity
      onPress={onPress}
      style={[styles.roundBtn, dark && { backgroundColor: DARK }]}
    >
      <Text style={{ fontSize: 16, color: dark ? '#fff' : DARK }}>{children}</Text>
    </TouchableOpacity>
  );
}

function CartBtn({ count = 2 }) {
  return (
    <View>
      <View style={[styles.roundBtn, { backgroundColor: DARK }]}>
        <Text style={{ fontSize: 16 }}>🛍️</Text>
      </View>
      <View style={styles.badge}>
        <Text style={styles.badgeText}>{count}</Text>
      </View>
    </View>
  );
}

function SignInScreen({ go }) {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [show, setShow] = useState(false);

  return (
    <View style={styles.flex}>
      <Header title="Вход" />
      <View style={styles.card}>
        <ScrollView showsVerticalScrollIndicator={false}>
          <Text style={styles.title}>С возвращением!</Text>
          <Text style={styles.subtitle}>Войдите, чтобы заказать вкусную еду</Text>

          <Illustration emoji="🍔" />

          <Input
            placeholder="Email"
            value={email}
            onChangeText={setEmail}
            keyboardType="email-address"
            autoCapitalize="none"
          />
          <View>
            <Input
              placeholder="Пароль"
              value={password}
              onChangeText={setPassword}
              secureTextEntry={!show}
            />
            <TouchableOpacity style={styles.eye} onPress={() => setShow(!show)}>
              <Text>{show ? '🙈' : '👁️'}</Text>
            </TouchableOpacity>
          </View>

          <TouchableOpacity onPress={() => go('forgot')}>
            <Text style={styles.forgot}>Забыли пароль?</Text>
          </TouchableOpacity>

          <Button
            title="Войти"
            disabled={!email || !password}
            onPress={() => go('home')}
          />

          <View style={styles.row}>
            <Text style={styles.small}>Нет аккаунта? </Text>
            <TouchableOpacity onPress={() => go('signup')}>
              <Text style={styles.link}>Регистрация</Text>
            </TouchableOpacity>
          </View>
        </ScrollView>
      </View>
    </View>
  );
}

function SignUpScreen({ go }) {
  const [name, setName] = useState('');
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [show, setShow] = useState(false);
  const [agree, setAgree] = useState(false);

  return (
    <View style={styles.flex}>
      <Header title="Регистрация" onBack={() => go('signin')} />
      <View style={styles.card}>
        <ScrollView showsVerticalScrollIndicator={false}>
          <Text style={styles.title}>Добро пожаловать!</Text>
          <Text style={styles.subtitle}>Привет, создайте новый аккаунт</Text>

          <Illustration emoji="🍕" />

          <Input placeholder="Имя" value={name} onChangeText={setName} />
          <Input
            placeholder="Email"
            value={email}
            onChangeText={setEmail}
            keyboardType="email-address"
            autoCapitalize="none"
          />
          <View>
            <Input
              placeholder="Пароль"
              value={password}
              onChangeText={setPassword}
              secureTextEntry={!show}
            />
            <TouchableOpacity style={styles.eye} onPress={() => setShow(!show)}>
              <Text>{show ? '🙈' : '👁️'}</Text>
            </TouchableOpacity>
          </View>

          <TouchableOpacity style={styles.checkRow} onPress={() => setAgree(!agree)}>
            <View style={[styles.checkbox, agree && styles.checkboxOn]}>
              {agree ? <Text style={{ color: '#fff', fontSize: 12 }}>✓</Text> : null}
            </View>
            <Text style={styles.small}>
              Создавая аккаунт, вы соглашаетесь с{' '}
              <Text style={styles.link}>Условиями использования</Text>
            </Text>
          </TouchableOpacity>

          <Button
            title="Зарегистрироваться"
            disabled={!name || !email || !password || !agree}
            onPress={() => go('verify')}
          />

          <View style={styles.row}>
            <Text style={styles.small}>Уже есть аккаунт? </Text>
            <TouchableOpacity onPress={() => go('signin')}>
              <Text style={styles.link}>Войти</Text>
            </TouchableOpacity>
          </View>
        </ScrollView>
      </View>
    </View>
  );
}

function ForgotScreen({ go }) {
  const [code, setCode] = useState('');

  return (
    <View style={styles.flex}>
      <Header title="Восстановление пароля" onBack={() => go('signin')} />
      <View style={styles.card}>
        <ScrollView showsVerticalScrollIndicator={false}>
          <Illustration emoji="🔒" />

          <Text style={styles.label}>Введите код</Text>
          <View style={styles.codeRow}>
            <TextInput
              style={[styles.input, { flex: 1, marginBottom: 0 }]}
              placeholder="Код"
              placeholderTextColor="#B0B0B0"
              value={code}
              onChangeText={setCode}
              keyboardType="number-pad"
              maxLength={4}
            />
            <TouchableOpacity
              style={styles.resend}
              onPress={() => Alert.alert('Отправлено', 'Код отправлен повторно')}
            >
              <Text style={styles.buttonText}>Отправить</Text>
            </TouchableOpacity>
          </View>

          <Text style={styles.info}>
            Мы отправили код на номер <Text style={styles.link}>+7 777 123 45 67</Text>
          </Text>
          <Text style={styles.info}>
            Код действителен 10 минут. Если сообщение не пришло, нажмите «Отправить».
          </Text>

          <Button
            title="Сменить пароль"
            disabled={code.length < 4}
            onPress={() => Alert.alert('Готово', 'Пароль успешно изменён ✅')}
          />

          <TouchableOpacity>
            <Text style={[styles.link, { textAlign: 'center', marginTop: 20 }]}>
              Изменить номер телефона
            </Text>
          </TouchableOpacity>
        </ScrollView>
      </View>
    </View>
  );
}

function VerifyScreen({ go }) {
  const [code, setCode] = useState('');
  const [sec, setSec] = useState(50);
  const inputRef = useRef(null);

  useEffect(() => {
    if (sec <= 0) return;
    const t = setTimeout(() => setSec(sec - 1), 1000);
    return () => clearTimeout(t);
  }, [sec]);

  return (
    <View style={styles.flex}>
      <Header title="Верификация" onBack={() => go('signup')} />
      <View style={styles.card}>
        <ScrollView showsVerticalScrollIndicator={false} keyboardShouldPersistTaps="handled">
          <Text style={styles.subtitle}>Мы отправили код на вашу почту</Text>
          <Text style={[styles.subtitle, { fontWeight: '700', color: DARK }]}>
            example@gmail.com
          </Text>

          <View style={styles.codeHead}>
            <Text style={styles.label}>КОД</Text>
            <TouchableOpacity
              disabled={sec > 0}
              onPress={() => setSec(50)}
            >
              <Text style={[styles.label, { textDecorationLine: 'underline' }]}>
                Отправить повторно{sec > 0 ? ` через ${sec} сек` : ''}
              </Text>
            </TouchableOpacity>
          </View>

          <TouchableOpacity
            activeOpacity={1}
            style={styles.boxesRow}
            onPress={() => inputRef.current && inputRef.current.focus()}
          >
            {[0, 1, 2, 3].map((i) => (
              <View
                key={i}
                style={[styles.codeBox, code.length === i && { borderColor: ORANGE }]}
              >
                <Text style={styles.codeDigit}>{code[i] || ''}</Text>
              </View>
            ))}
          </TouchableOpacity>

          <TextInput
            ref={inputRef}
            value={code}
            onChangeText={(t) => setCode(t.replace(/[^0-9]/g, ''))}
            keyboardType="number-pad"
            maxLength={4}
            style={{ height: 0, width: 0, opacity: 0 }}
            autoFocus
          />

          <Button
            title="ПОДТВЕРДИТЬ"
            disabled={code.length < 4}
            onPress={() => go('home')}
          />
        </ScrollView>
      </View>
    </View>
  );
}

const BURGERS = [
  { id: 1, name: 'Burger Bistro', place: 'Rose Garden', price: 40, emoji: '🍔' },
  { id: 2, name: "Smokin' Burger", place: 'Cafenio Restaurant', price: 60, emoji: '🍔' },
  { id: 3, name: 'Buffalo Burgers', place: 'Kaji Firm Kitchen', price: 75, emoji: '🍔' },
  { id: 4, name: 'Bullseye Burgers', place: 'Kabab Restaurant', price: 94, emoji: '🍔' },
];

const RESTAURANTS = [
  { id: 1, name: 'Pansi Restaurant', rating: 4.7, emoji: '🍽️' },
  { id: 2, name: 'American Spicy Burger Shop', rating: 4.3, emoji: '🍔' },
  { id: 3, name: 'Cafenio Coffee Club', rating: 4.0, emoji: '☕' },
];

const FAST_FOOD = [
  { id: 1, name: 'European Pizza', place: 'Uttora Coffe House', emoji: '🍕' },
  { id: 2, name: 'Buffalo Pizza', place: 'Cafenio Coffee Club', emoji: '🍕' },
];

function FoodCard({ item, onAdd }) {
  return (
    <View style={styles.foodCard}>
      <View style={styles.foodImg}>
        <Text style={{ fontSize: 48 }}>{item.emoji}</Text>
      </View>
      <Text style={styles.foodName} numberOfLines={1}>{item.name}</Text>
      <Text style={styles.foodPlace} numberOfLines={1}>{item.place}</Text>
      <View style={styles.foodBottom}>
        <Text style={styles.foodPrice}>${item.price}</Text>
        <TouchableOpacity style={styles.plus} onPress={onAdd}>
          <Text style={{ color: '#fff', fontWeight: '700' }}>+</Text>
        </TouchableOpacity>
      </View>
    </View>
  );
}

function HomeScreen({ go, cart, addToCart, openCategory }) {
  return (
    <View style={[styles.flex, styles.whiteBg]}>
      <ScrollView showsVerticalScrollIndicator={false} contentContainerStyle={{ padding: 20 }}>
        <View style={styles.topRow}>
          <RoundBtn onPress={() => go('signin')}>☰</RoundBtn>
          <View style={{ flex: 1, marginLeft: 12 }}>
            <Text style={styles.deliverTo}>ДОСТАВИТЬ В</Text>
            <Text style={styles.deliverPlace}>Halal Lab office ▾</Text>
          </View>
          <CartBtn count={cart} />
        </View>

        <Text style={styles.greet}>
          Привет, Халал, <Text style={{ fontWeight: '800' }}>добрый день!</Text>
        </Text>

        <TouchableOpacity style={styles.searchBox} onPress={() => go('search')}>
          <Text style={styles.searchText}>🔍  Поиск блюд, ресторанов</Text>
        </TouchableOpacity>

        <View style={styles.sectionRow}>
          <Text style={styles.sectionTitle}>Категории</Text>
          <TouchableOpacity onPress={() => go('burgers')}>
            <Text style={styles.seeAll}>Все ›</Text>
          </TouchableOpacity>
        </View>
        <ScrollView horizontal showsHorizontalScrollIndicator={false}>
          {[
            ['🍔', 'Бургеры', 'burger'],
            ['🍕', 'Пицца', 'pizza'],
            ['🥪', 'Сэндвичи', 'sandwich'],
            ['🌭', 'Хот-доги', 'hotdog'],
            ['🥗', 'Салаты', 'salad'],
          ].map(([e, n, k]) => (
            <TouchableOpacity key={n} style={styles.cat} onPress={() => openCategory(k)}>
              <Text style={{ fontSize: 22 }}>{e}</Text>
              <Text style={styles.catText}>{n}</Text>
            </TouchableOpacity>
          ))}
        </ScrollView>

        <View style={styles.sectionRow}>
          <Text style={styles.sectionTitle}>Открытые рестораны</Text>
          <TouchableOpacity onPress={() => go('burgers')}>
            <Text style={styles.seeAll}>Все ›</Text>
          </TouchableOpacity>
        </View>
        {RESTAURANTS.map((r) => (
          <View key={r.id} style={styles.restCard}>
            <View style={styles.restImg}>
              <Text style={{ fontSize: 44 }}>{r.emoji}</Text>
            </View>
            <Text style={styles.restName}>{r.name}</Text>
            <Text style={styles.restMeta}>⭐ {r.rating}   🚚 Бесплатно   🕒 20 мин</Text>
          </View>
        ))}

        <View style={[styles.sectionRow, { marginTop: 4 }]}>
          <Text style={styles.sectionTitle}>Популярные бургеры</Text>
          <TouchableOpacity onPress={() => go('burgers')}>
            <Text style={styles.seeAll}>Все ›</Text>
          </TouchableOpacity>
        </View>
        <ScrollView horizontal showsHorizontalScrollIndicator={false}>
          {BURGERS.map((b) => (
            <View key={b.id} style={{ width: 150, marginRight: 14 }}>
              <FoodCard item={b} onAdd={addToCart} />
            </View>
          ))}
        </ScrollView>
      </ScrollView>
    </View>
  );
}

function SearchScreen({ go, cart }) {
  const [q, setQ] = useState('');
  const keywords = ['Бургер', 'Сэндвич', 'Пицца', 'Сэндвичи'];

  const filteredRest = RESTAURANTS.filter((r) =>
    r.name.toLowerCase().includes(q.toLowerCase())
  );
  const filteredFood = FAST_FOOD.filter((f) =>
    f.name.toLowerCase().includes(q.toLowerCase())
  );

  return (
    <View style={[styles.flex, styles.whiteBg]}>
      <ScrollView
        showsVerticalScrollIndicator={false}
        contentContainerStyle={{ padding: 20 }}
        keyboardShouldPersistTaps="handled"
      >
        <View style={styles.topRow}>
          <RoundBtn onPress={() => go('home')}>‹</RoundBtn>
          <Text style={[styles.deliverPlace, { flex: 1, marginLeft: 12, fontSize: 16 }]}>
            Поиск
          </Text>
          <CartBtn count={cart} />
        </View>

        <View style={styles.searchBox}>
          <Text>🔍</Text>
          <TextInput
            style={styles.searchInput}
            placeholder="Пицца"
            placeholderTextColor="#A0A5BA"
            value={q}
            onChangeText={setQ}
          />
          {q ? (
            <TouchableOpacity onPress={() => setQ('')}>
              <Text style={{ color: '#A0A5BA' }}>✕</Text>
            </TouchableOpacity>
          ) : null}
        </View>

        <Text style={styles.sectionTitle}>Недавние запросы</Text>
        <ScrollView horizontal showsHorizontalScrollIndicator={false} style={{ marginTop: 12 }}>
          {keywords.map((k) => (
            <TouchableOpacity key={k} style={styles.chip} onPress={() => setQ(k)}>
              <Text style={styles.chipText}>{k}</Text>
            </TouchableOpacity>
          ))}
        </ScrollView>

        <Text style={[styles.sectionTitle, { marginTop: 22 }]}>Рекомендуемые рестораны</Text>
        {filteredRest.map((r) => (
          <TouchableOpacity key={r.id} style={styles.suggest} onPress={() => go('burgers')}>
            <View style={styles.suggestImg}>
              <Text style={{ fontSize: 22 }}>{r.emoji}</Text>
            </View>
            <View>
              <Text style={styles.suggestName}>{r.name}</Text>
              <Text style={styles.suggestRate}>⭐ {r.rating}</Text>
            </View>
          </TouchableOpacity>
        ))}
        {filteredRest.length === 0 && <Text style={styles.info}>Ничего не найдено</Text>}

        <Text style={[styles.sectionTitle, { marginTop: 22 }]}>Популярный фастфуд</Text>
        <View style={{ flexDirection: 'row', marginTop: 12 }}>
          {filteredFood.map((f) => (
            <View key={f.id} style={styles.fastCard}>
              <Text style={{ fontSize: 56 }}>{f.emoji}</Text>
              <Text style={styles.foodName}>{f.name}</Text>
              <Text style={styles.foodPlace}>{f.place}</Text>
            </View>
          ))}
        </View>
      </ScrollView>
    </View>
  );
}

function BurgersScreen({ go, cart, addToCart }) {
  return (
    <View style={[styles.flex, styles.whiteBg]}>
      <ScrollView showsVerticalScrollIndicator={false} contentContainerStyle={{ padding: 20 }}>
        <View style={styles.topRow}>
          <RoundBtn onPress={() => go('home')}>‹</RoundBtn>
          <TouchableOpacity style={styles.pill}>
            <Text style={styles.pillText}>БУРГЕР ▾</Text>
          </TouchableOpacity>
          <View style={{ flex: 1 }} />
          <RoundBtn dark onPress={() => go('search')}>🔍</RoundBtn>
          <View style={{ width: 8 }} />
          <RoundBtn>⚙️</RoundBtn>
        </View>

        <Text style={styles.sectionTitle}>Популярные бургеры</Text>
        <View style={styles.grid}>
          {BURGERS.map((b) => (
            <View key={b.id} style={styles.gridItem}>
              <FoodCard item={b} onAdd={addToCart} />
            </View>
          ))}
        </View>

        <Text style={[styles.sectionTitle, { marginTop: 10 }]}>Открытые рестораны</Text>
        <View style={styles.restCard}>
          <View style={[styles.restImg, { height: 140 }]}>
            <Text style={{ fontSize: 64 }}>🥞</Text>
          </View>
          <Text style={styles.restName}>Tasty Treat Gallery</Text>
          <Text style={styles.restMeta}>⭐ 4.7   🚚 Бесплатно   🕒 20 мин</Text>
        </View>
      </ScrollView>
    </View>
  );
}

const CATEGORY_LIST = [
  {
    key: 'pizza',
    name: 'Пицца',
    emoji: '🍕',
    heading: 'Популярная пицца',
    items: [
      { id: 1, name: 'European Pizza', place: 'Uttora Coffe House', price: 70, emoji: '🍕' },
      { id: 2, name: 'Buffalo Pizza', place: 'Cafenio Coffee Club', price: 85, emoji: '🍕' },
      { id: 3, name: 'Margherita', place: 'Pansi Restaurant', price: 90, emoji: '🍕' },
      { id: 4, name: 'Pepperoni', place: 'Rose Garden', price: 110, emoji: '🍕' },
    ],
    restaurants: [
      { id: 1, name: 'Uttora Coffe House', rating: 4.6 },
      { id: 2, name: 'Pansi Restaurant', rating: 4.7 },
    ],
  },
  {
    key: 'burger',
    name: 'Бургер',
    emoji: '🍔',
    heading: 'Популярные бургеры',
    items: [
      { id: 1, name: 'Burger Bistro', place: 'Rose Garden', price: 50, emoji: '🍔' },
      { id: 2, name: "Smokin' Burger", place: 'Cafenio Restaurant', price: 60, emoji: '🍔' },
      { id: 3, name: 'Buffalo Burgers', place: 'Kaji Firm Kitchen', price: 75, emoji: '🍔' },
      { id: 4, name: 'Bullseye Burgers', place: 'Kabab Restaurant', price: 94, emoji: '🍔' },
    ],
    restaurants: [
      { id: 1, name: 'American Spicy Burger Shop', rating: 4.3 },
      { id: 2, name: 'Rose Garden Restaurant', rating: 4.7 },
    ],
  },
  {
    key: 'sandwich',
    name: 'Сэндвичи',
    emoji: '🥪',
    heading: 'Популярные сэндвичи',
    items: [
      { id: 1, name: 'Club Sandwich', place: 'Kaji Firm Kitchen', price: 35, emoji: '🥪' },
      { id: 2, name: 'Chicken Sandwich', place: 'Pansi Restaurant', price: 42, emoji: '🥪' },
      { id: 3, name: 'Tuna Sandwich', place: 'Cafenio Coffee Club', price: 48, emoji: '🥪' },
      { id: 4, name: 'BLT Sandwich', place: 'Rose Garden', price: 55, emoji: '🥪' },
    ],
    restaurants: [
      { id: 1, name: 'Cafenio Coffee Club', rating: 4.0 },
      { id: 2, name: 'Kaji Firm Kitchen', rating: 4.4 },
    ],
  },
  {
    key: 'hotdog',
    name: 'Хот-доги',
    emoji: '🌭',
    heading: 'Популярные хот-доги',
    items: [
      { id: 1, name: 'Classic Hot Dog', place: 'Rose Garden', price: 25, emoji: '🌭' },
      { id: 2, name: 'Chili Dog', place: 'Kabab Restaurant', price: 32, emoji: '🌭' },
      { id: 3, name: 'Cheese Dog', place: 'Uttora Coffe House', price: 38, emoji: '🌭' },
      { id: 4, name: 'Jumbo Hot Dog', place: 'Kaji Firm Kitchen', price: 45, emoji: '🌭' },
    ],
    restaurants: [
      { id: 1, name: 'Kabab Restaurant', rating: 4.2 },
      { id: 2, name: 'Rose Garden Restaurant', rating: 4.7 },
    ],
  },
  {
    key: 'salad',
    name: 'Салаты',
    emoji: '🥗',
    heading: 'Популярные салаты',
    items: [
      { id: 1, name: 'Fresh Veggie Salad', place: 'Kaji Firm Kitchen', price: 28, emoji: '🥗' },
      { id: 2, name: 'Caesar Salad', place: 'Pansi Restaurant', price: 30, emoji: '🥗' },
      { id: 3, name: 'Greek Salad', place: 'Cafenio Coffee Club', price: 36, emoji: '🥗' },
      { id: 4, name: 'Chicken Salad', place: 'Rose Garden', price: 44, emoji: '🥗' },
    ],
    restaurants: [
      { id: 1, name: 'Pansi Restaurant', rating: 4.7 },
      { id: 2, name: 'Cafenio Coffee Club', rating: 4.0 },
    ],
  },
];

function CategoryScreen({ go, back, category, setCategory, addToCart }) {
  const cat = CATEGORY_LIST.find((c) => c.key === category) || CATEGORY_LIST[0];

  return (
    <View style={[styles.flex, styles.whiteBg]}>
      <ScrollView showsVerticalScrollIndicator={false} contentContainerStyle={{ padding: 20 }}>
        <View style={styles.topRow}>
          <RoundBtn onPress={() => go(back)}>‹</RoundBtn>
          <TouchableOpacity style={styles.pill}>
            <Text style={styles.pillText}>{cat.name.toUpperCase()} ▾</Text>
          </TouchableOpacity>
          <View style={{ flex: 1 }} />
          <RoundBtn dark onPress={() => go(back === 'home' ? 'search' : 'search2')}>🔍</RoundBtn>
          <View style={{ width: 8 }} />
          <RoundBtn>⚙️</RoundBtn>
        </View>

        <ScrollView
          horizontal
          showsHorizontalScrollIndicator={false}
          style={{ marginHorizontal: -20, marginBottom: 18 }}
          contentContainerStyle={{ paddingHorizontal: 20 }}
        >
          {CATEGORY_LIST.map((c) => {
            const active = c.key === cat.key;
            return (
              <TouchableOpacity
                key={c.key}
                style={[styles.chip, active && { backgroundColor: ORANGE, borderColor: ORANGE }]}
                onPress={() => setCategory(c.key)}
              >
                <Text style={[styles.chipText, active && { color: '#fff', fontWeight: '600' }]}>
                  {c.emoji}  {c.name}
                </Text>
              </TouchableOpacity>
            );
          })}
        </ScrollView>

        <Text style={styles.sectionTitle}>{cat.heading}</Text>
        <View style={styles.grid}>
          {cat.items.map((item) => (
            <View key={item.id} style={styles.gridItem}>
              <FoodCard item={item} onAdd={addToCart} />
            </View>
          ))}
        </View>

        <Text style={[styles.sectionTitle, { marginTop: 10 }]}>Рестораны</Text>
        <View style={{ marginTop: 14 }}>
          {cat.restaurants.map((r) => (
            <View key={r.id} style={styles.restCard}>
              <View style={[styles.restImg, { height: 140 }]}>
                <Text style={{ fontSize: 64 }}>{cat.emoji}</Text>
              </View>
              <Text style={styles.restName}>{r.name}</Text>
              <Text style={styles.restMeta}>⭐ {r.rating}   🚚 Бесплатно   🕒 20 мин</Text>
            </View>
          ))}
        </View>
      </ScrollView>
    </View>
  );
}

const RESTAURANTS2 = [
  { id: 1, name: 'Pansi Restaurant', rating: 4.7, emoji: '🍲' },
  { id: 2, name: 'American Spicy Burger Shop', rating: 4.3, emoji: '👨‍🍳' },
  { id: 3, name: 'Cafenio Coffee Club', rating: 4.0, emoji: '☕' },
];

const FAST_FOOD2 = [
  { id: 1, name: 'European Pizza', place: 'Uttora Coffe House', emoji: '🍕', tag: 'пицца' },
  { id: 2, name: 'Buffalo Pizza', place: 'Cafenio Coffee Club', emoji: '🍕', tag: 'пицца' },
  { id: 3, name: 'Smokin Burger', place: 'Cafenio Restaurant', emoji: '🍔', tag: 'бургер' },
  { id: 4, name: 'Club Sandwich', place: 'Kaji Firm Kitchen', emoji: '🥪', tag: 'сэндвич' },
];

function Home2Screen({ go, cart, openCategory }) {
  return (
    <View style={[styles.flex, styles.whiteBg]}>
      <ScrollView showsVerticalScrollIndicator={false} contentContainerStyle={{ padding: 20 }}>
        <View style={[styles.topRow, { marginTop: 8 }]}>
          <RoundBtn onPress={() => go('signin')}>☰</RoundBtn>
          <View style={{ flex: 1, marginLeft: 12 }}>
            <Text style={styles.deliverTo}>ДОСТАВИТЬ В</Text>
            <Text style={styles.deliverPlace}>Halal Lab office ▾</Text>
          </View>
          <CartBtn count={cart} />
        </View>

        <Text style={styles.greet}>
          Привет, Халал, <Text style={{ fontWeight: '800' }}>добрый день!</Text>
        </Text>

        <TouchableOpacity
          style={styles.searchBox}
          onPress={() => go('search2')}
          activeOpacity={0.8}
        >
          <Text style={{ color: '#A0A5BA' }}>🔍</Text>
          <Text style={[styles.searchText, { marginLeft: 10, fontSize: 13 }]}>
            Поиск блюд, ресторанов
          </Text>
        </TouchableOpacity>

        <View style={s2.sectionRow}>
          <Text style={s2.sectionTitle}>Все категории</Text>
          <TouchableOpacity onPress={() => go('burgers')}>
            <Text style={s2.seeAll}>Все  ›</Text>
          </TouchableOpacity>
        </View>
        <ScrollView
          horizontal
          showsHorizontalScrollIndicator={false}
          style={{ marginHorizontal: -20 }}
          contentContainerStyle={{ paddingHorizontal: 20, paddingTop: 46, paddingBottom: 18 }}
        >
          {CATEGORY_LIST.map((c) => (
            <TouchableOpacity
              key={c.key}
              style={s2.catCard}
              activeOpacity={0.85}
              onPress={() => openCategory(c.key)}
            >
              <Text style={s2.catEmoji}>{c.emoji}</Text>
              <Text style={s2.catName}>{c.name}</Text>
              <View style={s2.catBottom}>
                <Text style={s2.catStart}>От</Text>
                <Text style={s2.catPrice}>${Math.min(...c.items.map((i) => i.price))}</Text>
              </View>
            </TouchableOpacity>
          ))}
        </ScrollView>

        <View style={s2.sectionRow}>
          <Text style={s2.sectionTitle}>Открытые рестораны</Text>
          <TouchableOpacity onPress={() => go('burgers')}>
            <Text style={s2.seeAll}>Все  ›</Text>
          </TouchableOpacity>
        </View>

        <TouchableOpacity activeOpacity={0.9} onPress={() => go('burgers')}>
          <View style={s2.heroImg}>
            <Text style={{ fontSize: 84 }}>🥩</Text>
          </View>
          <Text style={s2.heroName}>Rose Garden Restaurant</Text>
          <Text style={s2.restTags}>Бургеры - Курица - Рис - Крылышки</Text>
          <View style={s2.metaRow}>
            <View style={s2.metaItem}>
              <Text style={s2.metaIcon}>☆</Text>
              <Text style={s2.metaBold}>4.7</Text>
            </View>
            <View style={s2.metaItem}>
              <Text style={s2.metaEmoji}>🚚</Text>
              <Text style={s2.metaText}>Бесплатно</Text>
            </View>
            <View style={s2.metaItem}>
              <Text style={s2.metaEmoji}>🕒</Text>
              <Text style={s2.metaText}>20 мин</Text>
            </View>
          </View>
        </TouchableOpacity>
      </ScrollView>
    </View>
  );
}

function Search2Screen({ go, cart }) {
  const [q, setQ] = useState('Пицца');
  const keywords = ['Бургер', 'Сэндвич', 'Пицца', 'Сэндвичи'];

  const query = q.trim().toLowerCase();
  const filteredFood = FAST_FOOD2.filter(
    (f) =>
      !query ||
      f.name.toLowerCase().includes(query) ||
      f.tag.includes(query) ||
      query.includes(f.tag)
  );

  return (
    <View style={[styles.flex, styles.whiteBg]}>
      <ScrollView
        showsVerticalScrollIndicator={false}
        contentContainerStyle={{ padding: 20 }}
        keyboardShouldPersistTaps="handled"
      >
        <View style={[styles.topRow, { marginTop: 8 }]}>
          <RoundBtn onPress={() => go('home2')}>‹</RoundBtn>
          <Text style={s2.topTitle}>Поиск</Text>
          <CartBtn count={cart} />
        </View>

        <View style={styles.searchBox}>
          <Text style={{ color: '#A0A5BA' }}>🔍</Text>
          <TextInput
            style={s2.searchInput}
            placeholder="Поиск блюд, ресторанов"
            placeholderTextColor="#A0A5BA"
            value={q}
            onChangeText={setQ}
          />
          {q ? (
            <TouchableOpacity style={s2.clearBtn} onPress={() => setQ('')}>
              <Text style={s2.clearText}>✕</Text>
            </TouchableOpacity>
          ) : null}
        </View>

        <Text style={s2.sectionTitle}>Недавние запросы</Text>
        <ScrollView
          horizontal
          showsHorizontalScrollIndicator={false}
          style={{ marginTop: 14, marginHorizontal: -20 }}
          contentContainerStyle={{ paddingHorizontal: 20, paddingBottom: 6 }}
        >
          {keywords.map((k, i) => (
            <TouchableOpacity key={k + i} style={s2.chip} onPress={() => setQ(k)}>
              <Text style={s2.chipText}>{k}</Text>
            </TouchableOpacity>
          ))}
        </ScrollView>

        <Text style={[s2.sectionTitle, { marginTop: 24 }]}>Рекомендуемые рестораны</Text>
        <View style={{ marginTop: 6 }}>
          {RESTAURANTS2.map((r) => (
            <TouchableOpacity key={r.id} style={s2.suggest} onPress={() => go('burgers')}>
              <View style={s2.suggestImg}>
                <Text style={{ fontSize: 26 }}>{r.emoji}</Text>
              </View>
              <View>
                <Text style={s2.suggestName}>{r.name}</Text>
                <View style={s2.rateRow}>
                  <Text style={s2.metaIcon}>☆</Text>
                  <Text style={s2.suggestRate}>{r.rating.toFixed(1)}</Text>
                </View>
              </View>
            </TouchableOpacity>
          ))}
        </View>

        <Text style={[s2.sectionTitle, { marginTop: 24 }]}>Популярный фастфуд</Text>
        {filteredFood.length === 0 ? (
          <Text style={[styles.info, { marginTop: 12 }]}>Ничего не найдено</Text>
        ) : (
          <ScrollView
            horizontal
            showsHorizontalScrollIndicator={false}
            style={{ marginHorizontal: -20 }}
            contentContainerStyle={{ paddingHorizontal: 20, paddingTop: 50, paddingBottom: 18 }}
          >
            {filteredFood.map((f) => (
              <TouchableOpacity
                key={f.id}
                style={s2.fastCard}
                activeOpacity={0.85}
                onPress={() => go('burgers')}
              >
                <Text style={s2.fastEmoji}>{f.emoji}</Text>
                <Text style={s2.fastName} numberOfLines={1}>{f.name}</Text>
                <Text style={s2.fastPlace} numberOfLines={1}>{f.place}</Text>
              </TouchableOpacity>
            ))}
          </ScrollView>
        )}
      </ScrollView>
    </View>
  );
}

const s2 = StyleSheet.create({
  sectionRow: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
    marginTop: 14,
  },
  sectionTitle: { fontSize: 20, fontWeight: '400', color: DARK },
  seeAll: { color: '#676767', fontSize: 14 },
  topTitle: { flex: 1, marginLeft: 14, fontSize: 17, color: DARK },

  catCard: {
    width: 120,
    backgroundColor: '#fff',
    borderRadius: 26,
    paddingTop: 58,
    paddingHorizontal: 14,
    paddingBottom: 14,
    marginRight: 20,
    shadowColor: '#3E4462',
    shadowOpacity: 0.12,
    shadowRadius: 14,
    shadowOffset: { width: 0, height: 8 },
    elevation: 5,
  },
  catEmoji: {
    position: 'absolute',
    top: -34,
    left: 0,
    right: 0,
    textAlign: 'center',
    fontSize: 78,
  },
  catName: { fontSize: 17, fontWeight: '700', color: DARK },
  catBottom: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
    marginTop: 8,
  },
  catStart: { fontSize: 13, color: '#A0A5BA' },
  catPrice: { fontSize: 14, fontWeight: '600', color: DARK },

  heroImg: {
    height: 190,
    borderRadius: 12,
    backgroundColor: '#E9E4DD',
    alignItems: 'center',
    justifyContent: 'center',
    marginTop: 12,
  },
  heroName: { fontSize: 20, fontWeight: '400', color: DARK, marginTop: 14 },
  restTags: { fontSize: 13, color: '#A5A7C2', marginTop: 6 },
  metaRow: { flexDirection: 'row', alignItems: 'center', marginTop: 14, marginBottom: 10 },
  metaItem: { flexDirection: 'row', alignItems: 'center', marginRight: 26 },
  metaIcon: { color: ORANGE, fontSize: 22, marginRight: 6 },
  metaEmoji: { fontSize: 18, marginRight: 8 },
  metaBold: { fontSize: 15, fontWeight: '700', color: DARK },
  metaText: { fontSize: 14, color: DARK },

  searchInput: { flex: 1, marginLeft: 10, fontSize: 14, color: DARK, padding: 0 },
  clearBtn: {
    width: 22,
    height: 22,
    borderRadius: 11,
    backgroundColor: '#C9CCD6',
    alignItems: 'center',
    justifyContent: 'center',
  },
  clearText: { color: '#fff', fontSize: 11, fontWeight: '700' },
  chip: {
    backgroundColor: '#fff',
    borderWidth: 1,
    borderColor: '#EDEDED',
    borderRadius: 30,
    paddingVertical: 12,
    paddingHorizontal: 26,
    marginRight: 12,
    shadowColor: '#3E4462',
    shadowOpacity: 0.06,
    shadowRadius: 8,
    shadowOffset: { width: 0, height: 3 },
    elevation: 1,
  },
  chipText: { fontSize: 15, color: '#464E57' },

  suggest: {
    flexDirection: 'row',
    alignItems: 'center',
    paddingVertical: 12,
    borderBottomWidth: 1,
    borderBottomColor: '#EBEBEB',
  },
  suggestImg: {
    width: 64,
    height: 52,
    borderRadius: 8,
    backgroundColor: '#E9E4DD',
    alignItems: 'center',
    justifyContent: 'center',
    marginRight: 14,
  },
  suggestName: { fontSize: 15, color: '#32343E' },
  rateRow: { flexDirection: 'row', alignItems: 'center', marginTop: 6 },
  suggestRate: { fontSize: 15, color: '#32343E' },

  fastCard: {
    width: 150,
    backgroundColor: '#fff',
    borderRadius: 24,
    paddingTop: 62,
    paddingHorizontal: 14,
    paddingBottom: 16,
    marginRight: 22,
    alignItems: 'center',
    shadowColor: '#3E4462',
    shadowOpacity: 0.12,
    shadowRadius: 14,
    shadowOffset: { width: 0, height: 8 },
    elevation: 5,
  },
  fastEmoji: {
    position: 'absolute',
    top: -38,
    left: 0,
    right: 0,
    textAlign: 'center',
    fontSize: 84,
  },
  fastName: { fontWeight: '700', fontSize: 14, color: DARK },
  fastPlace: { fontSize: 11, color: '#A0A5BA', marginTop: 4 },
});

export default function App() {
  const [screen, setScreen] = useState('signin');
  const [cart, setCart] = useState(2);
  const [category, setCategory] = useState('pizza');
  const [back, setBack] = useState('home');
  const addToCart = () => setCart((c) => c + 1);
  const openCategory = (key) => {
    setCategory(key);
    setBack(screen);
    setScreen('category');
  };

  const isAuth = ['signin', 'signup', 'forgot', 'verify'].includes(screen);

  return (
    <SafeAreaView style={[styles.safe, !isAuth && { backgroundColor: '#fff' }]}>
      <StatusBar style={isAuth ? 'light' : 'dark'} />
      <KeyboardAvoidingView
        style={styles.flex}
        behavior={Platform.OS === 'ios' ? 'padding' : undefined}
      >
        {screen === 'signin' && <SignInScreen go={setScreen} />}
        {screen === 'signup' && <SignUpScreen go={setScreen} />}
        {screen === 'forgot' && <ForgotScreen go={setScreen} />}
        {screen === 'verify' && <VerifyScreen go={setScreen} />}
        {screen === 'home' && (
          <HomeScreen go={setScreen} cart={cart} addToCart={addToCart} openCategory={openCategory} />
        )}
        {screen === 'search' && <SearchScreen go={setScreen} cart={cart} />}
        {screen === 'burgers' && (
          <BurgersScreen go={setScreen} cart={cart} addToCart={addToCart} />
        )}
        {screen === 'home2' && <Home2Screen go={setScreen} cart={cart} openCategory={openCategory} />}
        {screen === 'category' && (
          <CategoryScreen
            go={setScreen}
            back={back}
            category={category}
            setCategory={setCategory}
            addToCart={addToCart}
          />
        )}
        {screen === 'search2' && <Search2Screen go={setScreen} cart={cart} />}
      </KeyboardAvoidingView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  flex: { flex: 1 },
  whiteBg: { backgroundColor: '#fff' },
  safe: { flex: 1, backgroundColor: ORANGE },
  header: {
    height: 70,
    flexDirection: 'row',
    alignItems: 'center',
    paddingHorizontal: 20,
    paddingTop: 10,
  },
  back: { color: '#fff', fontSize: 36, marginRight: 12, marginTop: -4 },
  headerTitle: { color: '#fff', fontSize: 18, fontWeight: '600' },
  card: {
    flex: 1,
    backgroundColor: '#fff',
    borderTopLeftRadius: 30,
    borderTopRightRadius: 30,
    padding: 24,
  },
  title: { fontSize: 26, fontWeight: 'bold', color: ORANGE },
  subtitle: { fontSize: 13, color: '#666', marginTop: 4 },
  illustrationWrap: { alignItems: 'center', marginVertical: 24 },
  circle: {
    width: 130,
    height: 130,
    borderRadius: 65,
    backgroundColor: LIGHT_ORANGE,
    alignItems: 'center',
    justifyContent: 'center',
  },
  input: {
    borderWidth: 1,
    borderColor: '#E3E3E3',
    borderRadius: 10,
    paddingHorizontal: 14,
    paddingVertical: 12,
    fontSize: 15,
    marginBottom: 14,
    color: DARK,
  },
  eye: { position: 'absolute', right: 14, top: 13 },
  forgot: { textAlign: 'right', color: '#999', fontSize: 12, marginBottom: 20 },
  button: {
    backgroundColor: ORANGE,
    borderRadius: 10,
    paddingVertical: 14,
    alignItems: 'center',
    marginTop: 6,
  },
  buttonDisabled: { backgroundColor: '#FFD9A8' },
  buttonText: { color: '#fff', fontSize: 16, fontWeight: '600' },
  row: { flexDirection: 'row', justifyContent: 'center', marginTop: 20 },
  small: { fontSize: 13, color: '#444', flexShrink: 1 },
  link: { fontSize: 13, color: ORANGE, fontWeight: '600' },
  checkRow: { flexDirection: 'row', alignItems: 'center', marginBottom: 18, marginTop: 4 },
  checkbox: {
    width: 20,
    height: 20,
    borderWidth: 1.5,
    borderColor: ORANGE,
    borderRadius: 4,
    marginRight: 10,
    alignItems: 'center',
    justifyContent: 'center',
  },
  checkboxOn: { backgroundColor: ORANGE },
  label: { fontSize: 12, color: '#666', marginBottom: 8 },
  codeRow: { flexDirection: 'row', alignItems: 'center', marginBottom: 18 },
  resend: {
    backgroundColor: ORANGE,
    borderRadius: 10,
    paddingVertical: 13,
    paddingHorizontal: 16,
    marginLeft: 10,
  },
  info: { fontSize: 13, color: '#777', marginBottom: 10, lineHeight: 19 },

  codeHead: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    marginTop: 24,
  },
  boxesRow: { flexDirection: 'row', justifyContent: 'space-between', marginBottom: 24 },
  codeBox: {
    width: 64,
    height: 62,
    borderRadius: 12,
    backgroundColor: GRAY_BG,
    borderWidth: 1.5,
    borderColor: 'transparent',
    alignItems: 'center',
    justifyContent: 'center',
  },
  codeDigit: { fontSize: 20, fontWeight: '700', color: DARK },

  topRow: { flexDirection: 'row', alignItems: 'center', marginBottom: 20 },
  roundBtn: {
    width: 42,
    height: 42,
    borderRadius: 21,
    backgroundColor: GRAY_BG,
    alignItems: 'center',
    justifyContent: 'center',
  },
  badge: {
    position: 'absolute',
    top: -4,
    right: -4,
    width: 20,
    height: 20,
    borderRadius: 10,
    backgroundColor: ORANGE,
    alignItems: 'center',
    justifyContent: 'center',
  },
  badgeText: { color: '#fff', fontSize: 11, fontWeight: '700' },
  deliverTo: { color: ORANGE, fontSize: 11, fontWeight: '800' },
  deliverPlace: { color: '#676767', fontSize: 14, marginTop: 2 },
  greet: { fontSize: 16, color: DARK, marginBottom: 16 },
  searchBox: {
    flexDirection: 'row',
    alignItems: 'center',
    backgroundColor: GRAY_BG,
    borderRadius: 12,
    paddingHorizontal: 16,
    paddingVertical: 14,
    marginBottom: 22,
  },
  searchText: { color: '#A0A5BA', fontSize: 14 },
  searchInput: { flex: 1, marginLeft: 10, fontSize: 14, color: DARK },

  sectionRow: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
    marginTop: 16,
    marginBottom: 12,
  },
  sectionTitle: { fontSize: 18, fontWeight: '600', color: DARK },
  seeAll: { color: '#676767', fontSize: 14 },

  cat: {
    flexDirection: 'row',
    alignItems: 'center',
    backgroundColor: '#fff',
    borderRadius: 30,
    paddingVertical: 8,
    paddingHorizontal: 14,
    marginRight: 10,
    marginBottom: 6,
    shadowColor: '#000',
    shadowOpacity: 0.08,
    shadowRadius: 8,
    shadowOffset: { width: 0, height: 3 },
    elevation: 3,
  },
  catText: { marginLeft: 8, fontWeight: '600', color: DARK },

  foodCard: {
    backgroundColor: '#fff',
    borderRadius: 16,
    padding: 12,
    shadowColor: '#000',
    shadowOpacity: 0.08,
    shadowRadius: 10,
    shadowOffset: { width: 0, height: 4 },
    elevation: 3,
  },
  foodImg: { alignItems: 'center', justifyContent: 'center', height: 80 },
  foodName: { fontWeight: '700', fontSize: 13, color: DARK, marginTop: 6 },
  foodPlace: { fontSize: 11, color: '#A0A5BA', marginTop: 2 },
  foodBottom: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
    marginTop: 8,
  },
  foodPrice: { fontWeight: '700', fontSize: 14, color: DARK },
  plus: {
    width: 26,
    height: 26,
    borderRadius: 13,
    backgroundColor: ORANGE,
    alignItems: 'center',
    justifyContent: 'center',
  },
  grid: { flexDirection: 'row', flexWrap: 'wrap', justifyContent: 'space-between', marginTop: 14 },
  gridItem: { width: '48%', marginBottom: 16 },

  restCard: { marginBottom: 18 },
  restImg: {
    height: 120,
    borderRadius: 14,
    backgroundColor: LIGHT_ORANGE,
    alignItems: 'center',
    justifyContent: 'center',
  },
  restName: { fontSize: 18, fontWeight: '600', color: DARK, marginTop: 10 },
  restMeta: { fontSize: 12, color: '#676767', marginTop: 4 },

  chip: {
    borderWidth: 1,
    borderColor: '#EDEDED',
    borderRadius: 30,
    paddingVertical: 8,
    paddingHorizontal: 16,
    marginRight: 10,
  },
  chipText: { fontSize: 13, color: '#464E57' },
  suggest: {
    flexDirection: 'row',
    alignItems: 'center',
    paddingVertical: 10,
    borderBottomWidth: 1,
    borderBottomColor: '#EBEBEB',
  },
  suggestImg: {
    width: 56,
    height: 46,
    borderRadius: 8,
    backgroundColor: LIGHT_ORANGE,
    alignItems: 'center',
    justifyContent: 'center',
    marginRight: 12,
  },
  suggestName: { fontSize: 14, color: '#32343E' },
  suggestRate: { fontSize: 13, color: '#32343E', marginTop: 4 },
  fastCard: {
    width: '46%',
    marginRight: '4%',
    alignItems: 'center',
    backgroundColor: '#fff',
    borderRadius: 16,
    padding: 12,
    shadowColor: '#000',
    shadowOpacity: 0.06,
    shadowRadius: 8,
    elevation: 2,
  },

  pill: {
    marginLeft: 10,
    borderWidth: 1,
    borderColor: '#EDEDED',
    borderRadius: 30,
    paddingVertical: 10,
    paddingHorizontal: 16,
  },
  pillText: { fontSize: 12, fontWeight: '700', color: DARK },
});
