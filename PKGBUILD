# Maintainer: Sreejith <vector@vectorspace.xyz>

pkgname=tree-sitter-markdown-noicb
pkgver=0.5.1
pkgrel=1
pkgdesc='Markdown grammar for tree-sitter: no [i]ndented [c]ode [b]locks'
arch=(x86_64)
url=https://github.com/vectorspacexyz/tree-sitter-markdown
license=(MIT)
groups=(tree-sitter-grammars)
conflicts=(tree-sitter-markdown)
makedepends=(
  cmake
  git
  tree-sitter-cli
)
optdepends=('tree-sitter: core library')
provides=(
  "tree-sitter-markdown=$pkgver"
  "libtree-sitter-markdown.so"
  "libtree-sitter-markdown-inline.so"
)
source=("https://github.com/vectorspacexyz/tree-sitter-markdown/archive/refs/heads/split_parser.zip")
sha256sums=('SKIP')

prepare() {
  cd tree-sitter-markdown-split_parser/tree-sitter-markdown
  tree-sitter generate src/grammar.json

  cd ../tree-sitter-markdown-inline
  tree-sitter generate src/grammar.json
}

build() {
  cd tree-sitter-markdown-split_parser
  local cmake_options=(
    -B build
    -S .
    -W no-dev
    -D CMAKE_BUILD_TYPE=None
    -D CMAKE_INSTALL_PREFIX=/usr
  )
  cmake "${cmake_options[@]}"
  cmake --build build
}

package() {
  install -d "$pkgdir"/usr/lib/tree_sitter
  ln -s /usr/lib/libtree-sitter-markdown.so \
    "$pkgdir"/usr/lib/tree_sitter/markdown.so
  ln -s /usr/lib/libtree-sitter-markdown-inline.so \
    "$pkgdir"/usr/lib/tree_sitter/markdown_inline.so

  cd tree-sitter-markdown-split_parser
  DESTDIR="$pkgdir" cmake --install build

  install -Dm644 -t "$pkgdir"/usr/share/doc/$pkgname README.md
  install -Dm644 -t "$pkgdir"/usr/share/licenses/$pkgname LICENSE
}
