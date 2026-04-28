# Fadil-
Action: file_editor create /app/frontend/app/role-select.tsx --file-text "import React, { useState } from 'react';
import { View, Text, StyleSheet, TouchableOpacity, ActivityIndicator, Alert } from 'react-native';
import { SafeAreaView } from 'react-native-safe-area-context';
import { User, Wrench, ChevronRight } from 'lucide-react-native';
import { useRouter } from 'expo-router';
import { theme } from '../src/theme';
import { api } from '../src/api';
import { useAuth } from '../src/auth';

export default function RoleSelect() {
  const router = useRouter();
  const { refresh } = useAuth();
  const [busy, setBusy] = useState<string | null>(null);

  const choose = async (role: 'consumer' | 'mechanic') => {
    setBusy(role);
    try {
      await api('/api/users/role', { method: 'POST', body: JSON.stringify({ role }) });
      await refresh();
      router.replace(role === 'consumer' ? '/(consumer)/home' : '/(mechanic)/dashboard');
    } catch (e: any) {
      Alert.alert('Gagal', e?.message || 'Coba lagi');
    } finally { setBusy(null); }
  };

  return (
    <SafeAreaView style={styles.c} testID=\"role-select-screen\">
      <View style={styles.header}>
        <Text style={styles.label}>STEP 1/1</Text>
        <Text style={styles.h1}>Kamu mau{\"\n\"}pakai sebagai apa?</Text>
        <Text style={styles.sub}>Pilih peran kamu. Kamu bisa ubah nanti lewat profil.</Text>
      </View>

      <View style={styles.roles}>
        <TouchableOpacity
          testID=\"role-consumer-button\"
          style={styles.roleCard}
          onPress={() => choose('consumer')}
          disabled={!!busy}
          activeOpacity={0.85}
        >
          <View style={[styles.iconBox, { backgroundColor: theme.colors.primary }]}>
            <User size={32} color={theme.colors.primaryFg} strokeWidth={2.2} />
          </View>
          <View style={{ flex: 1 }}>
            <Text style={styles.roleTitle}>Saya Pelanggan</Text>
            <Text style={styles.roleDesc}>Panggil montir ke lokasi saya</Text>
          </View>
          {busy === 'consumer' ? <ActivityIndicator color={theme.colors.primary} /> : <ChevronRight size={22} color={theme.colors.textSecondary} />}
        </TouchableOpacity>

        <TouchableOpacity
          testID=\"role-mechanic-button\"
          style={styles.roleCard}
          onPress={() => choose('mechanic')}
          disabled={!!busy}
          activeOpacity={0.85}
        >
          <View style={[styles.iconBox, { backgroundColor: theme.colors.surfaceElevated, borderWidth: 2, borderColor: theme.colors.primary }]}>
            <Wrench size={30} color={theme.colors.primary} strokeWidth={2.2} />
          </View>
          <View style={{ flex: 1 }}>
            <Text style={styles.roleTitle}>Saya Montir</Text>
            <Text style={styles.roleDesc}>Cari orderan & dapat penghasilan</Text>
          </View>
          {busy === 'mechanic' ? <ActivityIndicator color={theme.colors.primary} /> : <ChevronRight size={22} color={theme.colors.textSecondary} />}
        </TouchableOpacity>
      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  c: { flex: 1, backgroundColor: theme.colors.background, paddingHorizontal: 20 },
  header: { marginTop: 48, marginBottom: 40 },
  label: { fontFamily: 'PlusJakartaSans_700Bold', color: theme.colors.primary, letterSpacing: 1.5, fontSize: 11, marginBottom: 10 },
  h1: { fontFamily: 'SpaceGrotesk_700Bold', fontSize: 30, color: theme.colors.textPrimary, letterSpacing: -0.8, lineHeight: 34 },
  sub: { fontFamily: 'PlusJakartaSans_400Regular', fontSize: 14, color: theme.colors.textSecondary, marginTop: 10 },
  roles: { gap: 14 },
  roleCard: { flexDirection: 'row', alignItems: 'center', gap: 16, backgroundColor: theme.colors.surface, borderWidth: 1, borderColor: theme.colors.border, borderRadius: 8, padding: 20 },
  iconBox: { width: 60, height: 60, borderRadius: 8, alignItems: 'center', justifyContent: 'center' },
  roleTitle: { fontFamily: 'SpaceGrotesk_700Bold', color: theme.colors.textPrimary, fontSize: 18 },
  roleDesc: { fontFamily: 'PlusJakartaSans_400Regular', color: theme.colors.textSecondary, fontSize: 13, marginTop: 4 },
});
"
Observation: Create successful: /app/frontend/app/role-select.tsx

Fetching debug logs for expo

==> /var/log/supervisor/expo.err.log <==
λ  WARN  Image: style.resizeMode is deprecated. Please use props.resizeMode. 
λ  WARN  Image: style.resizeMode is deprecated. Please use props.resizeMode. 
Error: Premature close
    at onclose (node:internal/streams/end-of-stream:159:30)
    at processTicksAndRejections (node:internal/process/task_queues:77:11)
    at runNextTicks (node:internal/process/task_queues:64:3)
    at processImmediate (node:internal/timers:454:9)
    at process.callbackTrampoline (node:internal/async_hooks:130:17)
Error: Premature close
    at onclose (node:internal/streams/end-of-stream:159:30)
    at processTicksAndRejections (node:internal/process/task_queues:77:11)
λ  WARN  Image: style.resizeMode is deprecated. Please use props.resizeMode. 
λ  WARN  Image: style.resizeMode is deprecated. Please use props.resizeMode. 

==> /var/log/supervisor/expo.out.log <==
λ node_modules/expo-router/node/render.js ░░░░░░░░░░░░░░░░  0.0% (0/1)
Web node_modules/expo-router/entry.js ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓░ 99.7% (747/748)
λ node_modules/expo-router/node/render.js ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓░ 98.9% (701/713)
Web node_modules/expo-router/entry.js ░░░░░░░░░░░░░░░░  0.0% (0/1)
λ node_modules/expo-router/node/render.js ░░░░░░░░░░░░░░░░  0.0% (0/1)
Web Bundled 96847ms node_modules/expo-router/entry.js (748 modules)
Web Bundled 82018ms node_modules/expo-router/entry.js (1 module)
λ Bundled 97728ms node_modules/expo-router/node/render.js (717 modules)
λ Bundled 82998ms node_modules/expo-router/node/render.js (1 module)
λ  LOG  https://6ebbddb5-6d75-49b3-8d76-065e2672d9b7.preview.emergentagent.com EXPO_PUBLIC_BACKEND_URL
λ  LOG  https://6ebbddb5-6d75-49b3-8d76-065e2672d9b7.preview.emergentagent.com EXPO_PUBLIC_BACKEND_URL
Web node_modules/expo-router/entry.js ░░░░░░░░░░░░░░░░  0.0% (0/1)
λ Bundled 122ms node_modules/expo-router/node/render.js (1 module)
λ  LOG  https://6ebbddb5-6d75-49b3-8d76-065e2672d9b7.preview.emergentagent.com EXPO_PUBLIC_BACKEND_URL
Web node_modules/expo-router/entry.js ░░░░░░░░░░░░░░░░  0.0% (0/1)
Web Bundled 1237ms node_modules/expo-router/entry.js (1 module)
λ Bundled 108ms node_modules/expo-router/node/render.js (1 module)
λ  LOG  https://6ebbddb5-6d75-49b3-8d76-065e2672d9b7.preview.emergentagent.com EXPO_PUBLIC_BACKEND_URL
Web node_modules/expo-router/entry.js ░░░░░░░░░░░░░░░░  0.0% (0/1)
Web Bundled 761ms node_modules/expo-router/entry.js (1 module)


Fetching debug logs for backend

==> /var/log/supervisor/backend.err.log <==
INFO:     Will watch for changes in these directories: ['/app/backend']
INFO:     Uvicorn running on http://0.0.0.0:8001 (Press CTRL+C to quit)
INFO:     Started reloader process [191] using WatchFiles
INFO:     Started server process [222]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
WARNING:  WatchFiles detected changes in 'server.py'. Reloading...
INFO:     Shutting down
INFO:     Waiting for application shutdown.
INFO:     Application shutdown complete.
INFO:     Finished server process [222]
INFO:     Started server process [533]
INFO:     Waiting for application startup.
2026-04-28 02:34:19,753 - server - INFO - Seeded mock users
INFO:     Application startup complete.

==> /var/log/supervisor/backend.out.log <==


Fetching debug logs for mongodb

tail: cannot open '/var/log/supervisor/mongodb*.log' for reading: No such file or directory
