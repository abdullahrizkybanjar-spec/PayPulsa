// app/page.tsx
'use client'
import { useState, useEffect } from 'react'
import { Tabs, TabsContent, TabsList, TabsTrigger } from '@/components/ui/tabs'
import { Input } from '@/components/ui/input'
import { Button } from '@/components/ui/button'
import { Card, CardContent, CardFooter, CardHeader, CardTitle } from '@/components/ui/card'
import { Badge } from '@/components/ui/badge'
import { Loader2, Smartphone, Wifi, Zap, Gamepad2, ChevronRight, Shield, ZapIcon, Clock, CheckCircle } from 'lucide-react'

// Mock data untuk produk populer
const popularProducts = [
  { id: 1, name: 'Pulsa 10.000', price: 11000, category: 'pulsa', description: 'Pulsa semua operator' },
  { id: 2, name: 'Paket Data 5GB', price: 25000, category: 'data', description: 'Masa aktif 30 hari' },
  { id: 3, name: 'Token Listrik 50.000', price: 50000, category: 'pln', description: 'Token listrik pra-bayar' },
  { id: 4, name: 'Voucher Mobile Legends', price: 15000, category: 'game', description: '86 Diamond' },
]

export default function Home() {
  const [number, setNumber] = useState('')
  const [category, setCategory] = useState('pulsa')
  const [products, setProducts] = useState<any[]>([])
  const [loading, setLoading] = useState(false)
  const [selectedProduct, setSelectedProduct] = useState<any>(null)
  const [showConfirmation, setShowConfirmation] = useState(false)

  // Fetch products ketika number atau category berubah
  useEffect(() => {
    if (number && number.length > 10) {
      setLoading(true)
      // Simulasi fetch data
      setTimeout(() => {
        const mockProducts = {
          pulsa: [
            { id: 1, code: 'p5', name: 'Pulsa 5.000', price: 6000, description: 'Pulsa semua operator' },
            { id: 2, code: 'p10', name: 'Pulsa 10.000', price: 11000, description: 'Pulsa semua operator' },
            { id: 3, code: 'p25', name: 'Pulsa 25.000', price: 26000, description: 'Pulsa semua operator' },
            { id: 4, code: 'p50', name: 'Pulsa 50.000', price: 51000, description: 'Pulsa semua operator' },
          ],
          data: [
            { id: 5, code: 'd1', name: 'Paket 1GB', price: 15000, description: '1GB 7 hari' },
            { id: 6, code: 'd3', name: 'Paket 3GB', price: 25000, description: '3GB 30 hari' },
            { id: 7, code: 'd5', name: 'Paket 5GB', price: 35000, description: '5GB 30 hari' },
            { id: 8, code: 'd10', name: 'Paket 10GB', price: 50000, description: '10GB 30 hari' },
          ],
          pln: [
            { id: 9, code: 't20', name: 'Token 20.000', price: 20000, description: 'Token Listrik' },
            { id: 10, code: 't50', name: 'Token 50.000', price: 50000, description: 'Token Listrik' },
            { id: 11, code: 't100', name: 'Token 100.000', price: 100000, description: 'Token Listrik' },
            { id: 12, code: 't200', name: 'Token 200.000', price: 200000, description: 'Token Listrik' },
          ],
          game: [
            { id: 13, code: 'g10', name: 'Voucher 10.000', price: 10000, description: 'Mobile Legends, PUBG, Free Fire' },
            { id: 14, code: 'g20', name: 'Voucher 20.000', price: 20000, description: 'Mobile Legends, PUBG, Free Fire' },
            { id: 15, code: 'g50', name: 'Voucher 50.000', price: 50000, description: 'Mobile Legends, PUBG, Free Fire' },
            { id: 16, code: 'g100', name: 'Voucher 100.000', price: 100000, description: 'Mobile Legends, PUBG, Free Fire' },
          ]
        }
        setProducts(mockProducts[category as keyof typeof mockProducts] || [])
        setLoading(false)
      }, 1000)
    } else {
      setProducts([])
    }
  }, [category, number])

  const handleProductSelect = (product: any) => {
    setSelectedProduct(product)
    setShowConfirmation(true)
  }

  const handlePayment = async () => {
    // Simulasi pembayaran
    setShowConfirmation(false)
    // Redirect ke halaman pembayaran
  }

  const getCategoryIcon = (cat: string) => {
    switch (cat) {
      case 'pulsa': return <Smartphone className="h-5 w-5" />
      case 'data': return <Wifi className="h-5 w-5" />
      case 'pln': return <Zap className="h-5 w-5" />
      case 'game': return <Gamepad2 className="h-5 w-5" />
      default: return <Smartphone className="h-5 w-5" />
    }
  }

  return (
    <div className="min-h-screen bg-gradient-to-b from-blue-50 to-white">
      {/* Header */}
      <header className="bg-white shadow-sm">
        <div className="container mx-auto px-4 py-4 flex justify-between items-center">
          <div className="flex items-center space-x-2">
            <ZapIcon className="h-8 w-8 text-blue-600" />
            <span className="text-2xl font-bold text-blue-600">DigiPay</span>
          </div>
          <nav className="hidden md:flex space-x-8">
            <a href="#" className="text-gray-700 hover:text-blue-600 font-medium">Beranda</a>
            <a href="#" className="text-gray-700 hover:text-blue-600 font-medium">Produk</a>
            <a href="#" className="text-gray-700 hover:text-blue-600 font-medium">Promo</a>
            <a href="#" className="text-gray-700 hover:text-blue-600 font-medium">Bantuan</a>
          </nav>
          <div className="flex space-x-4">
            <Button variant="outline">Masuk</Button>
            <Button>Daftar</Button>
          </div>
        </div>
      </header>

      <main>
        {/* Hero Section */}
        <section className="py-16 bg-gradient-to-r from-blue-600 to-purple-600 text-white">
          <div className="container mx-auto px-4 text-center">
            <h1 className="text-4xl md:text-5xl font-bold mb-4">Top Up & Bayar Tagihan</h1>
            <p className="text-xl mb-8 max-w-2xl mx-auto">Beli pulsa, paket data, token listrik, dan voucher game dengan mudah dan cepat</p>
            
            {/* Quick Purchase Form */}
            <div className="max-w-2xl mx-auto bg-white rounded-xl shadow-lg p-6 text-gray-800">
              <Tabs defaultValue="pulsa" onValueChange={setCategory} className="w-full">
                <TabsList className="grid grid-cols-4 mb-6">
                  <TabsTrigger value="pulsa" className="flex items-center space-x-2">
                    <Smartphone className="h-4 w-4" />
                    <span>Pulsa</span>
                  </TabsTrigger>
                  <TabsTrigger value="data" className="flex items-center space-x-2">
                    <Wifi className="h-4 w-4" />
                    <span>Data</span>
                  </TabsTrigger>
                  <TabsTrigger value="pln" className="flex items-center space-x-2">
                    <Zap className="h-4 w-4" />
                    <span>Listrik</span>
                  </TabsTrigger>
                  <TabsTrigger value="game" className="flex items-center space-x-2">
                    <Gamepad2 className="h-4 w-4" />
                    <span>Game</span>
                  </TabsTrigger>
                </TabsList>
                
                <TabsContent value={category}>
                  <div className="space-y-4">
                    <div>
                      <label className="block text-sm font-medium mb-2 text-left">
                        {category === 'pln' ? 'ID Pelanggan / No. Meter' : 'Nomor Handphone'}
                      </label>
                      <Input
                        placeholder={category === 'pln' ? 'Contoh: 12345678901' : 'Contoh: 081234567890'}
                        value={number}
                        onChange={(e) => setNumber(e.target.value)}
                        className="py-3"
                      />
                    </div>
                  </div>
                </TabsContent>
              </Tabs>
            </div>
          </div>
        </section>

        {/* Product List Section */}
        {number && (
          <section className="py-12 bg-white">
            <div className="container mx-auto px-4">
              <h2 className="text-2xl font-bold mb-6">Pilihan Produk</h2>
              
              {loading ? (
                <div className="flex justify-center py-12">
                  <Loader2 className="h-8 w-8 animate-spin text-blue-600" />
                </div>
              ) : (
                <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                  {products.map((product) => (
                    <Card key={product.id} className="hover:shadow-lg transition-shadow">
                      <CardHeader className="pb-3">
                        <CardTitle className="text-lg">{product.name}</CardTitle>
                      </CardHeader>
                      <CardContent className="pb-3">
                        <p className="text-gray-600 text-sm">{product.description}</p>
                        <p className="text-xl font-bold text-blue-600 mt-2">Rp {product.price.toLocaleString('id-ID')}</p>
                      </CardContent>
                      <CardFooter>
                        <Button 
                          className="w-full" 
                          onClick={() => handleProductSelect(product)}
                        >
                          Beli Sekarang
                        </Button>
                      </CardFooter>
                    </Card>
                  ))}
                </div>
              )}
            </div>
          </section>
        )}

        {/* Popular Products Section */}
        {!number && (
          <section className="py-12 bg-gray-50">
            <div className="container mx-auto px-4">
              <div className="flex justify-between items-center mb-6">
                <h2 className="text-2xl font-bold">Produk Populer</h2>
                <a href="#" className="text-blue-600 flex items-center">
                  Lihat Semua <ChevronRight className="h-4 w-4 ml-1" />
                </a>
              </div>
              
              <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                {popularProducts.map((product) => (
                  <Card key={product.id} className="hover:shadow-lg transition-shadow">
                    <CardHeader className="pb-3">
                      <div className="flex justify-between items-start">
                        <CardTitle className="text-lg">{product.name}</CardTitle>
                        <Badge variant="secondary" className="flex items-center">
                          {getCategoryIcon(product.category)}
                        </Badge>
                      </div>
                    </CardHeader>
                    <CardContent className="pb-3">
                      <p className="text-gray-600 text-sm">{product.description}</p>
                      <p className="text-xl font-bold text-blue-600 mt-2">Rp {product.price.toLocaleString('id-ID')}</p>
                    </CardContent>
                    <CardFooter>
                      <Button 
                        className="w-full" 
                        onClick={() => {
                          setCategory(product.category)
                          setNumber('08123456789') // Set contoh nomor
                        }}
                      >
                        Beli Sekarang
                      </Button>
                    </CardFooter>
                  </Card>
                ))}
              </div>
            </div>
          </section>
        )}

        {/* Features Section */}
        <section className="py-12 bg-white">
          <div className="container mx-auto px-4">
            <h2 className="text-2xl font-bold text-center mb-12">Mengapa Memilih DigiPay?</h2>
            
            <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
              <div className="text-center">
                <div className="bg-blue-100 w-16 h-16 rounded-full flex items-center justify-center mx-auto mb-4">
                  <Zap className="h-8 w-8 text-blue-600" />
                </div>
                <h3 className="text-xl font-semibold mb-2">Proses Cepat</h3>
                <p className="text-gray-600">Transaksi selesai dalam hitungan detik, tanpa perlu menunggu lama</p>
              </div>
              
              <div className="text-center">
                <div className="bg-blue-100 w-16 h-16 rounded-full flex items-center justify-center mx-auto mb-4">
                  <Shield className="h-8 w-8 text-blue-600" />
                </div>
                <h3 className="text-xl font-semibold mb-2">Aman & Terpercaya</h3>
                <p className="text-gray-600">Sistem keamanan berlapis melindungi setiap transaksi Anda</p>
              </div>
              
              <div className="text-center">
                <div className="bg-blue-100 w-16 h-16 rounded-full flex items-center justify-center mx-auto mb-4">
                  <Clock className="h-8 w-8 text-blue-600" />
                </div>
                <h3 className="text-xl font-semibold mb-2">24/7 Tersedia</h3>
                <p className="text-gray-600">Layanan kami tersedia setiap saat, kapanpun Anda membutuhkan</p>
              </div>
            </div>
          </div>
        </section>

        {/* How to Use Section */}
        <section className="py-12 bg-gray-50">
          <div className="container mx-auto px-4">
            <h2 className="text-2xl font-bold text-center mb-12">Cara Melakukan Pembelian</h2>
            
            <div className="grid grid-cols-1 md:grid-cols-4 gap-8">
              <div className="text-center">
                <div className="bg-blue-600 text-white w-12 h-12 rounded-full flex items-center justify-center mx-auto mb-4 text-xl font-bold">1</div>
                <h3 className="text-lg font-semibold mb-2">Pilih Produk</h3>
                <p className="text-gray-600">Pilih kategori dan produk yang ingin Anda beli</p>
              </div>
              
              <div className="text-center">
                <div className="bg-blue-600 text-white w-12 h-12 rounded-full flex items-center justify-center mx-auto mb-4 text-xl font-bold">2</div>
                <h3 className="text-lg font-semibold mb-2">Masukkan Nomor</h3>
                <p className="text-gray-600">Masukkan nomor handphone atau ID pelanggan</p>
              </div>
              
              <div className="text-center">
                <div className="bg-blue-600 text-white w-12 h-12 rounded-full flex items-center justify-center mx-auto mb-4 text-xl font-bold">3</div>
                <h3 className="text-lg font-semibold mb-2">Bayar</h3>
                <p className="text-gray-600">Lakukan pembayaran dengan metode yang tersedia</p>
              </div>
              
              <div className="text-center">
                <div className="bg-blue-600 text-white w-12 h-12 rounded-full flex items-center justify-center mx-auto mb-4 text-xl font-bold">4</div>
                <h3 className="text-lg font-semibold mb-2">Selesai</h3>
                <p className="text-gray-600">Produk akan langsung dikirim ke tujuan Anda</p>
              </div>
            </div>
          </div>
        </section>
      </main>

      {/* Footer */}
      <footer className="bg-gray-800 text-white py-12">
        <div className="container mx-auto px-4">
          <div className="grid grid-cols-1 md:grid-cols-4 gap-8">
            <div>
              <div className="flex items-center space-x-2 mb-4">
                <ZapIcon className="h-8 w-8 text-blue-400" />
                <span className="text-2xl font-bold">DigiPay</span>
              </div>
              <p className="text-gray-400">Platform terpercaya untuk pembelian produk digital dengan proses cepat dan aman.</p>
            </div>
            
            <div>
              <h3 className="text-lg font-semibold mb-4">Layanan</h3>
              <ul className="space-y-2">
                <li><a href="#" className="text-gray-400 hover:text-white">Pulsa</a></li>
                <li><a href="#" className="text-gray-400 hover:text-white">Paket Data</a></li>
                <li><a href="#" className="text-gray-400 hover:text-white">Token Listrik</a></li>
                <li><a href="#" className="text-gray-400 hover:text-white">Voucher Game</a></li>
              </ul>
            </div>
            
            <div>
              <h3 className="text-lg font-semibold mb-4">Bantuan</h3>
              <ul className="space-y-2">
                <li><a href="#" className="text-gray-400 hover:text-white">Cara Pembelian</a></li>
                <li><a href="#" className="text-gray-400 hover:text-white">FAQ</a></li>
                <li><a href="#" className="text-gray-400 hover:text-white">Syarat & Ketentuan</a></li>
                <li><a href="#" className="text-gray-400 hover:text-white">Kebijakan Privasi</a></li>
              </ul>
            </div>
            
            <div>
              <h3 className="text-lg font-semibold mb-4">Kontak Kami</h3>
              <ul className="space-y-2">
                <li className="text-gray-400">Email: support@digipay.com</li>
                <li className="text-gray-400">WhatsApp: +62 812 3456 7890</li>
                <li className="text-gray-400">Telegram: @digipay_support</li>
              </ul>
            </div>
          </div>
          
          <div className="border-t border-gray-700 mt-8 pt-8 text-center text-gray-400">
            <p>© 2023 DigiPay. All rights reserved.</p>
          </div>
        </div>
      </footer>

      {/* Confirmation Modal */}
      {showConfirmation && selectedProduct && (
        <div className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
          <div className="bg-white rounded-lg max-w-md w-full p-6">
            <h3 className="text-xl font-bold mb-4">Konfirmasi Pembelian</h3>
            
            <div className="space-y-4">
              <div>
                <p className="text-gray-600">Produk</p>
                <p className="font-semibold">{selectedProduct.name}</p>
              </div>
              
              <div>
                <p className="text-gray-600">Nomor Tujuan</p>
                <p className="font-semibold">{number}</p>
              </div>
              
              <div>
                <p className="text-gray-600">Harga</p>
                <p className="font-semibold text-blue-600">Rp {selectedProduct.price.toLocaleString('id-ID')}</p>
              </div>
            </div>
            
            <div className="flex space-x-4 mt-6">
              <Button 
                variant="outline" 
                className="flex-1" 
                onClick={() => setShowConfirmation(false)}
              >
                Batal
              </Button>
              <Button 
                className="flex-1" 
                onClick={handlePayment}
              >
                Bayar Sekarang
              </Button>
            </div>
          </div>
        </div>
      )}
    </div>
  )
}
