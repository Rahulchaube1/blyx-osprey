<img src="assets/logo.png" width="112" height="112" alt="Osprey logo">

# Osprey

Score a detection against a reference after clipping both to the camera frame. This Blyx workflow framework is part of the vision, audio and speech collection.

An out-of-frame detection can change IoU even when the visible pixels agree. Clip both boxes before evaluating their overlap. [OpenCV, rectangle coordinates](https://docs.opencv.org/4.x/d2/d44/classcv_1_1Rect__.html)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-osprey.git
cd blyx-osprey
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-osprey) · [Package page](https://www.blyx-lang.space/packages/osprey) · [Handbook](https://doc.blyx-lang.space/guide/osprey)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-osprey.git vendor/osprey
```

```blyx
use vendor::osprey::osprey;

fn main() {
    let pred = [-2, 0, 2, 2];
    let truth = [0, 0, 4, 2];
    let width = 4.0;
    let height = 4.0;
    let threshold = 0.5;
    let result = osprey_compare(pred, truth, width, height, threshold);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
0.5
1
4
```

## API

`osprey_compare(pred, truth, width, height, threshold)`

Returns [visible IoU, matched, visible intersection area]. Match requires positive overlap and a score at least equal to the threshold. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| pred | Vector of values, each a finite number |
| truth | Vector of values, each a finite number |
| width | A positive finite number |
| height | A positive finite number |
| threshold | A probability in [0,1] |

## Run the command-line project

Run the example with your own numbers. Vector arguments accept up to 16 comma-separated entries; use `[]` for an empty vector. The imported API accepts longer vectors. Invalid arguments return a nonzero exit status.

```sh
blyxc native-run project.blyx -- "-2,0,2,2" "0,0,4,2" 4 4 0.5
```

## Libraries

- [BoxOverlap](https://github.com/Rahulchaube1/blyx-boxoverlap/tree/v0.1.0) — Measure intersection and union of two axis-aligned image boxes.
- [BoxClip](https://github.com/Rahulchaube1/blyx-boxclip/tree/v0.1.0) — Clip a detection rectangle to the visible image.

This release includes identical copies of both library modules so a tagged clone can build offline.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-osprey/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). The package artwork uses [Lucide icons](https://lucide.dev/license); see [artwork notices](assets/NOTICE.txt).

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
