# 颜色 - colors

object - color - level
![](Tailwindcss/attachments/Pasted%20image%2020251205220810.png)
## Text

```tsx
	<p className='text-black'>helloworld</p>

	<p className='text-red-600'>hello world</p>

	<p className='text-gray-500'>helloworld</p>
```

![](Tailwindcss/attachments/Pasted%20image%2020251205214746.png)

## Background

```tsx
	<div className='bg-slate-700'>

		<p className='text-red-600'>hello world</p>

	</div>
```

![](Tailwindcss/attachments/Pasted%20image%2020251205214913.png)

## Text Underline

```tsx
                <p className='underline decoration-gray-600 text-red-600'>hello world</p>

                <p className='underline text-red-600'>hello world</p>
```

![](Tailwindcss/attachments/Pasted%20image%2020251205215307.png)

## border

```tsx
<input className='border-red-600 border-2'/>
```

![](Tailwindcss/attachments/Pasted%20image%2020251205215648.png)

## divide

```tsx
                <div className='divide-y divide-red-600'>

                    <div>Item 1</div>

                    <div>Item 2</div>

                    <div>Item 3</div>

                    <div>Item 4</div>

                    <div>Item 5</div>

                </div>
```

![](Tailwindcss/attachments/Pasted%20image%2020251205220234.png)

## Outline

```tsx
                <button className='outline outline-red-600'>

                    Sumbit

                </button>
```

![](Tailwindcss/attachments/Pasted%20image%2020251205220554.png)

## Shadow

```tsx
                <button className='outline outline-red-600'>

                    Sumbit

                </button>
```

![](Tailwindcss/attachments/Pasted%20image%2020251205221021.png)

## accent

```tsx
            <input

                className='accent-pink-500'

                type='checkbox'

            />

            Option1

            <input

                className='accent-red-300'

                type='checkbox'

            />

            Option2
```

![](Tailwindcss/attachments/Pasted%20image%2020251205221325.png)

## Arbitrary

```tsx
<p className='text-[#fb8500]'>www.51cloudclass.com</p>
```

![](Tailwindcss/attachments/Pasted%20image%2020251205221741.png)


# 容器空间 - container-spacing

![](Tailwindcss/attachments/Pasted%20image%2020251206130933.png)

## margin

```tsx
            <div className='mb-12 bg-slate-100'>mb-4</div>

            <div className='m-4 bg-slate-100'>m-4</div>

            <div className='mx-12 bg-slate-100'>mx-4</div>

            <div className='my-12 bg-slate-100'>my-4</div>
```

![](Tailwindcss/attachments/Pasted%20image%2020251206132258.png)

## padding

```tsx
            <div className='py-12 bg-slate-100'>py-12</div>

            <div className='p-4 bg-slate-500'>p-12</div>
```

![](Tailwindcss/attachments/Pasted%20image%2020251206132321.png)

## space

```tsx
            {/* Space Between X */}

            <div className='space-x-4 flex'>

                <div className='bg-red-100'>01</div>

                <div className='bg-red-200'>02</div>

                <div className='bg-red-300'>03</div>

            </div>

            {/* Space Between Y */}

            <div className='space-y-4'>

                <div className='bg-red-100'>01</div>

                <div className='bg-red-200'>02</div>

                <div className='bg-red-300'>03</div>

            </div>
```

![](Tailwindcss/attachments/Pasted%20image%2020251206132411.png)

# 字体样式 - typography

![](attachments/Pasted%20image%2020251206133253.png)

## font
```tsx
            {/* Font Family  */}

            <p className='font-sans'>font-sans</p>

            <p className='font-mono'>font-mono</p>

            <p className='font-serif'>font-serif</p>

  

            {/* Font Size  */}

            <p className='text-base'>text-base</p>

            <p className='text-2xl'>text-2xl</p>

            <p className='text-3xl'>text-3xl</p>

  

            {/* Font Weight  */}

            <p className='font-extralight text-3xl'>font-extralight text-3xl</p>

            <p className='font-semibold text-3xl'>font-semibold text-3xl</p>
```

![](attachments/Pasted%20image%2020251206134941.png)

## letter

```tsx
            <p className='tracking-tighter font-semibold text-3xl'>

                tracking-tighter font-semibold text-3xl

            </p>

            <p className='tracking-widest font-semibold text-3xl'>

                tracking-widest font-semibold text-3xl

            </p>
```

![](attachments/Pasted%20image%2020251206135010.png)

---

```tsx
            {/* Text Alignment  */}

            <p className='text-right font-semibold text-3xl bg-slate-300'>

                text-right font-semibold text-3xl bg-slate-300

            </p>

            <p className='text-center font-semibold text-3xl bg-slate-500'>

                text-center font-semibold text-3xl bg-slate-500

            </p>
```

![](attachments/Pasted%20image%2020251206135123.png)

```tsx
            {/* Text Decoration  */}

            <p className='text-center font-semibold text-3xl underline decoration-4'>

                text-center font-semibold text-3xl underline decoration-4

            </p>

  

            {/* Decoration Style  */}

            <p className='underline decoration-dotted text-left font-semibold text-3xl'>

                underline decoration-dotted text-left font-semibold text-3xl

            </p>

            <p className='underline decoration-wavy decoration-orange-400 text-left font-semibold text-3xl'>

                underline decoration-wavy decoration-orange-400 text-left font-semibold text-3xl

            </p>

  

            {/* Decoration Offset  */}

            <p className='underline underline-offset-8 text-left font-semibold text-3xl'>

                underline underline-offset-8 text-left font-semibold text-3xl

            </p>
```

![](attachments/Pasted%20image%2020251206135247.png)

```tsx
            {/* Text Transform -- */}

            <p className='text-left font-semibold text-3xl'>

                text-left font-semibold text-3xl

            </p>

            <p className='capitalize text-left font-semibold text-3xl'>

                capitalize text-left font-semibold text-3xl

            </p>
```

![](attachments/Pasted%20image%2020251206135306.png)

# 大小 - sizing

```tsx
            {/* Width */}

            <div className='bg-slate-100 w-20'>bg-slate-100 w-20</div>

            <div className='bg-slate-200 w-60'>bg-slate-200 w-60</div>

            {/* Percentages */}

            <div className='bg-slate-300 w-1/2'>bg-slate-300 w-1/2</div>

  

            {/* Width of the viewport */}

            {/* <div className='bg-slate-500 w-screen'>www.51cloudclass.com</div> */}

  

            {/* 100% of container */}

            <div className='bg-slate-300 w-full'>bg-slate-300 w-full</div>

  

            {/* min/max content */}

            <div className='bg-orange-200 w-min'>

                <p>bg-orange-200 w-min Lorem ipsum dolor</p>

            </div>

            <div className='bg-orange-400 w-fit'>

                <p>bg-orange-400 w-fit Lorem ipsum dolor www.51cloudclass.com</p>

            </div>

            <div className='bg-orange-600 w-max'>

                <p>bg-orange-600 w-max Lorem ipsum dolor www.51cloudclass.com</p>

                <p>Lorem ipsum dolor</p>

            </div>

  

            {/* Arbitrary width */}

            <div className='w-[385px] bg-indigo-200'>

                <p>w-[385px] bg-indigo-200 Lorem ipsum dolor www.51cloudclass.com</p>

            </div>

  

            {/* Max Width */}

            <div className='min-w-[400px] max-w-md bg-indigo-400'>

                <p>min-w-[400px] max-w-md bg-indigo-400 Lorem ipsum dolor www.51cloudclass.com</p>

            </div>
```

![](attachments/Pasted%20image%2020251206145112.png)

```tsx
            {/* Height (Most of the same options as widths) */}

            <div className='h-10 bg-amber-200'>

                <p>h-10 bg-amber-200 Lorem ipsum dolor www.51cloudclass.com</p>

            </div>

            {/* Min Height */}

            <div className='min-h-fit bg-amber-400'>

                <p>min-h-fit bg-amber-400 Lorem ipsum dolor www.51cloudclass.com</p>

            </div>

            {/* Max Height */}

  

            {/* Full screen height */}

            <div className='h-screen bg-amber-600'>

                <p>h-screen bg-amber-600 Lorem ipsum dolor www.51cloudclass.com</p>

            </div>
```

![](attachments/Pasted%20image%2020251206145202.png)

# 布局位置 - layout position

```tsx
            <div className='grandpa relative h-60 w-full bg-slate-400'>

                <h1>grandpa</h1>

                <div className='parent ml-40 w-4/5 bg-orange-300'>

                    <h2>parent</h2>

                    <div className='children absolute top-0 bg-red-300'>

                        Lorem ipsum dolor sit amet consectetur adipisicing elit. Laboriosam,

                        voluptatum!

                    </div>

                </div>

            </div>

  

            {/* Top left corner */}

            <div className='relative h-20 w-4/5 bg-orange-300'>

                <div className='absolute top-0 left-40 bg-red-300'>top left corner</div>

            </div>

  

            {/* Top right corner */}

  

            {/* Bottom left corner */}

  

            {/* Bottom right corner */}

            <div className='relative h-20 w-4/5 bg-orange-300'>

                <div className='absolute bottom-0 right-40 bg-red-300'>

                    top left corner

                </div>

            </div>

  

            {/* Span top edge */}

            <div className='relative h-20 w-4/5 bg-orange-300'>

                <div className='absolute top-0 inset-y-0 right-40 bg-red-300'>

                    span top corner

                </div>

            </div>
            {/* Span left edge */}

            {/* Span right edge */}

            {/* Span bottom edge */}

            {/* Display Classes */}
```

![](attachments/Pasted%20image%2020251206165255.png)

```tsx
            {/* Display Classes */}

            <div>

                <p>

                    Lorem ipsum dolor sit amet consectetur, adipisicing elit. Nobis

                    veritatis cumque minus recusandae fugit dicta

                    <span className='inline-block p-20 h-40 w-40 bg-red-300'>

                        inline 01

                    </span>

                    suscipit ipsam beatae architecto enim. Lorem ipsum dolor sit amet

                    consectetur adipisicing elit. Similique iste tempora nesciunt, aliquam

                    doloremque non! Autem voluptas architecto mollitia sint.

                </p>

            </div>

  

            <button

                className='p-4 bg-slate-500 shadow-md'

                onClick={() => setShow(!show)}

            >

                Toggle show

            </button>

            <div className={show ? 'hidden' : 'block'}>

                <h1>display: none</h1>

            </div>
```

![](attachments/Pasted%20image%2020251206165426.png)

```tsx
            {/* Z-Index */}

            <div className='flex'>

                <div className='h-40 w-40 bg-orange-300 hover:z-10 '></div>

                <div className='h-40 w-40 bg-red-300 -ml-20 hover:z-10'></div>

            </div>
```

![](attachments/Pasted%20image%2020251206165457.png)

```tsx
            {/* Floats */}

            <div>

                <p>

                    Lorem ipsum dolor sit amet consectetur adipisicing elit. Similique

                    voluptatibus consequuntur nesciunt.

                    <img

                        className='h-20 w-20 float-left m-10'

                        src='/assets/img/img1.jpg'

                        alt=''

                    />

                    Perferendis autem quaerat dolorem quos ex eum numquam?

                </p>

            </div>
```

![](attachments/Pasted%20image%2020251206165519.png)

# 背景和阴影 - backgrounds-shadows

```tsx
        <div className='space-y-20'>

            <h2 className=' text-2xl'>Background Shadows</h2>

            {/* Background Classes */}

            <div

                className='h-96 w-96 bg-blue-300 bg-cover bg-right bg-no-repeat'

                style={{ backgroundImage: 'url("/background-sea.jpg")' }}

            ></div>

  

            {/* Gradients */}

            <div className='text-white text-center leading-10  h-12 w-30 bg-gradient-to-bl from-slate-800 to-red-300'>

                Click me

            </div>

  

            {/* Shadows */}

            <div className='shadow-lg bg-red-400 flex justify-center items-center'>

                Submit

            </div>

            {/* Mix Blend */}

            <div className='h-20 w-full'></div>

        </div>
```

![](attachments/Pasted%20image%2020251206171546.png)

# 边框样式 - border

```tsx
            {/* Border Width & Colors */}

  

            <div className='w-1/2 m-3 p-5 border rounded-lg shadow-lg z-10'>

                Lorem ipsum dolor sit amet, consectetur adipisicing elit. Commodi,

                doloribus!

            </div>

  

            <div className='w-1/2 m-3 p-5 border-2 rounded-lg shadow-lg z-10'>

                Lorem ipsum dolor sit amet, consectetur adipisicing elit. Commodi,

                doloribus!

            </div>

  

            <div className='w-1/2 m-3 p-5 border-y-0 border-x-2 border-indigo-500 rounded-lg shadow-lg z-10'>

                Lorem ipsum dolor sit amet, consectetur adipisicing elit. Commodi,

                doloribus!

            </div>
```

![](attachments/Pasted%20image%2020251206172904.png)

```tsx
            {/* Border Radius */}

            <div>

                <img

                    className='rounded-full h-20 w-20 border-2 border-red-400 shadow-md'

                    src='/background-sea.jpg'

                />

            </div>
```

![](attachments/Pasted%20image%2020251206172923.png)

```tsx
            {/* Outline */}

            <div className='border text-center shadow-lg hover:shadow-sm'>Submit</div>
```

![](attachments/Pasted%20image%2020251206172945.png)

# 滤镜效果 - filters

```tsx
            {/* Blur */}

            <div className='blur-[1px] hover:blur-none'>

                Lorem ipsum dolor sit amet consectetur adipisicing elit. Doloribus esse

                quam culpa voluptates eum. A molestiae similique voluptatum in nesciunt!

            </div>

            {/* Brightness */}

            <div className='brightness-50'>

                <img

                    className='w-48 h-auto'

                    src='/assets/img/img3.jpg'

                    alt=''

                />

            </div>

            <div className='brightness-110'>

                <img

                    className='w-48 h-auto'

                    src='/assets/img/img3.jpg'

                    alt=''

                />

            </div>

  

            {/* Contrast */}

            <div className='contrast-75'>

                <img

                    className='w-48 h-auto'

                    src='/assets/img/img3.jpg'

                    alt=''

                />

            </div>
```

![](attachments/Pasted%20image%2020251207102219.png)

```tsx
{/* Grayscale */}

            <div className='grayscale-[100%]'>

                <img

                    className='w-48 h-auto'

                    src='/assets/img/img3.jpg'

                    alt=''

                />

                <p className='text-indigo-500'>

                    Lorem ipsum dolor, sit amet consectetur adipisicing elit. In,

                    veritatis.

                </p>

            </div>

  

            {/* Invert */}

  

            {/* Sepia */}

  

            {/* Hue Rotate */}

            <div className='-hue-rotate-30'>

                <img

                    className='w-48 h-auto'

                    src='/assets/img/img3.jpg'

                    alt=''

                />

            </div>
```

![](attachments/Pasted%20image%2020251207102245.png)

# 用户交互 - interactivity

```tsx
            {/* Hover State Styling */}

            <button

                type='button'

                className='

                hover:bg-orange-500 hover:text-white

                hover:-translate-y-1

                duration-300

                rounded-lg bg-black text-white

                shadow-xl

                py-3 px-5'

            >

                Submit

            </button>

  

            {/* Focus State Styling */}

            <button

                type='button'

                className='

                focus:bg-green-500

                duration-300

                rounded-lg bg-black text-white

                shadow-xl

                py-3 px-5'

            >

                Submit

            </button>

  

            {/* Active State Styling */}

            <button

                type='button'

                className='

                active:bg-orange-500

                duration-300

                rounded-lg bg-black text-white

                shadow-xl

                py-3 px-5'

            >

                Submit

            </button>
```


![](attachments/Pasted%20image%2020251207104951.png)

```tsx
{/* Styling based on parent state */}

            <a

                href='#'

                className='

                group p-6 shadow-lg hover:bg-sky-500

                rounded-lg

                bg-white'

            >

                <div className='group-hover:text-red-500'>

                    <h3>Card Title</h3>

                </div>

                <p className='group-hover:text-cyan-400'>This is some card text</p>

            </a>
```

![](attachments/Pasted%20image%2020251207105019.png)

```tsx
            {/* Pseudo Classes */}

            <ul>

                <li className='even:bg-green-200 odd:bg-blue-200'>Item 1</li>

                <li className='even:bg-green-200 odd:bg-blue-200'>Item 2</li>

                <li className='even:bg-green-200 odd:bg-blue-200'>Item 3</li>

                <li className='even:bg-green-200 odd:bg-blue-200'>Item 4</li>

                <li className='even:bg-green-200 odd:bg-blue-200'>Item 5</li>

                <li className='even:bg-green-200 odd:bg-blue-200'>Item 6</li>

                <li className='even:bg-green-200 odd:bg-blue-200'>Item 7</li>

                <li className='even:bg-green-200 odd:bg-blue-200'>Item 8</li>

                <li className='even:bg-green-200 odd:bg-blue-200'>Item 9</li>

                <li className='even:bg-green-200 odd:bg-blue-200'>Item 10</li>

            </ul>
```

![](attachments/Pasted%20image%2020251207105043.png)

```tsx
            <div id='top'></div>

            <a href='#footer'>Scroll to footer</a>
            
            <a
                href='#top'
                className='border p-5 shadow-lg'>
                scroll to top
            </a>

            <div id='footer'> Footer </div>
```

# 设备分辨率 - breakpoints

```tsx
            <div

                className='

            w-screen h-32 bg-black

            sm:bg-green-800

            md:bg-blue-800

            lg:bg-yellow-800

            xl:bg-purple-800

            '

            >

                <p className='text-2xl font-bold p-6 text-white'>

                    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Debitis,

                    corporis.

                </p>

                <img

                    className='hidden lg:block '

                    src='/background-sea.jpg'

                    alt=''

                />

            </div>
```

![](attachments/Pasted%20image%2020251207110554.png)


# 列布局 - column layouts

```tsx
<div className='columns-2 gap-8'>

                <img

                    className='w-full'

                    src='/assets/img/img1.jpg'

                    alt=''

                />

                <img

                    className='w-full'

                    src='/assets/img/img2.jpg'

                    alt=''

                />

                <img

                    className='w-full break-after-column'

                    src='/assets/img/img3.jpg'

                    alt=''

                />

                <img

                    className='w-full'

                    src='/assets/img/img4.jpg'

                    alt=''

                />

            </div>
```

![](attachments/Pasted%20image%2020251207130023.png)

```tsx
<div className='columns-3 gap-24'>

                <img

                    className='w-full'

                    src='/assets/img/img3.jpg'

                />

                <img

                    className='w-full break-before-column'

                    src='/assets/img/img4.jpg'

                />

                <img

                    className='w-full'

                    src='/assets/img/img5.jpg'

                />

                <img

                    className='w-full'

                    src='/assets/img/img6.jpg'

                />

                <img

                    className='w-full'

                    src='/assets/img/img7.jpg'

                />

            </div>
```

![](attachments/Pasted%20image%2020251207130058.png)

```tsx
            <div className='columns-3xs'>

                <img

                    className='w-full aspect-video'

                    src='/assets/img/img8.jpg'

                />

                <img

                    className='w-full aspect-square'

                    src='/assets/img/img9.jpg'

                />

                <img

                    className='w-full break'

                    src='/assets/img/img1.jpg'

                />

                <img

                    className='w-full '

                    src='/assets/img/img2.jpg'

                />

            </div>
```

![](attachments/Pasted%20image%2020251207130121.png)


# 弹性盒子布局 - flexbox

```tsx
            <div

                className='flex flex-row

            justify-around

            items-center

            flex-wrap

            bg-orange-400 w-screen h-72'

            >

                <div className='h-32 p-10 border border-blue-600 bg-blue-100'>01</div>

                <div className='h-32 p-10 border border-blue-600 bg-blue-100'>02</div>

                <div className='self-start h-32 p-10 border border-blue-600 bg-blue-100'>

                    03

                </div>

                <div className='self-end h-32 p-10 border border-blue-600 bg-blue-100'>

                    04

                </div>

            </div>
```

![](attachments/Pasted%20image%2020251207161332.png)

```tsx
            {/* Flex Column, Gap and Order */}

            <div className='flex flex-col gap-4 w-screen bg-gray-200 items-center'>

                <div className='order-4 p-10 border border-pink-600'>01</div>

                <div className='order-1 p-10 border border-pink-600'>02</div>

                <div className='p-10 border border-pink-600'>03</div>

                <div className='p-10 border border-pink-600'>04</div>

            </div>
```

![](attachments/Pasted%20image%2020251207161357.png)

```tsx
            {/* Grow and shrink */}

            <div className='flex w-screen bg-gray-300 flex-wrap flex-row-reverse'>

                <div className='flex-none p-10 w-64 border border-blue-600 bg-blue-100'>

                    01

                </div>

                <div className='flex-initial p-10 w-64 border border-blue-600 bg-blue-100'>

                    02

                </div>

                <div className='flex-1 p-10 w-64 border border-blue-600 bg-blue-100'>

                    03

                </div>

                <div className='flex-1 p-10 w-64 border border-blue-600 bg-blue-100'>

                    04

                </div>

            </div>
```

![](attachments/Pasted%20image%2020251207161416.png)


# 网络布局 - grid

```tsx
            {/* Grid cols and rows */}

            <div className='grid grid-cols-3 grid-rows-4 w-screen'>

                <div className='p-10 border border-blue-600 bg-blue-100'>Item 1</div>

                <div className='p-10 border border-blue-600 bg-blue-100'>Item 2</div>

                <div className='p-10 border border-blue-600 bg-blue-100'>Item 3</div>

                <div className='p-10 border border-blue-600 bg-blue-100'>Item 4</div>

                <div className='p-10 border border-blue-600 bg-blue-100'>Item 5</div>

                <div className='p-10 border border-blue-600 bg-blue-100'>Item 6</div>

                <div className='p-10 border border-blue-600 bg-blue-100'>Item 7</div>

                <div className='p-10 border border-blue-600 bg-blue-100'>Item 8</div>

                <div className='p-10 border border-blue-600 bg-blue-100'>Item 9</div>

            </div>
```

![](attachments/Pasted%20image%2020251207162401.png)

```tsx
            {/* Col and row span */}

            <div className='grid grid-cols-3 gap-4 w-screen bg-gray-200'>

                <div className='col-span-2 row-span-2 p-10 border border-cyan-600 bg-cyan-100'>

                    Item 01

                </div>

                <div className='p-10 border border-cyan-600 bg-cyan-100'>Item 02</div>

                <div className='p-10 border border-cyan-600 bg-cyan-100'>Item 03</div>

                <div className='p-10 border border-cyan-600 bg-cyan-100'>Item 04</div>

                <div className='p-10 border border-cyan-600 bg-cyan-100'>Item 05</div>

                <div className='p-10 border border-cyan-600 bg-cyan-100'>Item 06</div>

                <div className='p-10 border border-cyan-600 bg-cyan-100'>Item 07</div>

                <div className='p-10 border border-cyan-600 bg-cyan-100'>Item 08</div>

                <div className='p-10 border border-cyan-600 bg-cyan-100'>Item 09</div>

            </div>
```

![](attachments/Pasted%20image%2020251207162421.png)

# 动画变形及过渡 - transform and transition

```tsx
            {/* No transition */}

            <button className='px-8 py-2 m-24 text-white bg-blue-500 rounded hover:bg-blue-700'>

                Click me

            </button>

  

            {/* Transition */}

            <button

                className='

            transition-colors

            duration-700

            hover:scale-110

            px-8 py-2 m-24 text-white bg-blue-500 rounded hover:bg-blue-700'

            >

                Click me

            </button>

  

            {/* Transition and Transform */}

            <button

                className='

            transition-colors

            ease-in-out

            delay-150

            duration-1000

            hover:scale-110

            px-8 py-2 m-24 text-white bg-blue-500 rounded hover:bg-blue-700'

            >

                Click me

            </button>
```

![](attachments/Pasted%20image%2020251207163817.png)

```tsx
            {/* Transform and Transition */}

            <img

                src='/assets/img/img1.jpg'

                alt=''

                className='

                hover:transform hover:rotate-180 transition

                delay-1000 duration-[4s]

                hover:scale-75 hover:skew-x-12 aspect-square

                '

            />
```

![](attachments/Pasted%20image%2020251207163840.png)

# 辐射式动画、跳跃式动画、弹珠式动画、脉冲式动画 - animation

```tsx
            {/* animate-spin */}

            <div className='flex items-center justify-center'>

                <button

                    type='button'

                    className='py-2 px-4

                inline-flex gap-4 items-center

                shadow rounded-md

                bg-indigo-500 hover:bg-indigo-400

                transition ease-in-out duration-150

                cursor-not-allowed

                text-white

                font-bold

                '

                    disabled

                >

                    <svg

                        className='h-10 w-10 animate-spin'

                        viewBox='0 0 1024 1024'

                        version='1.1'

                        xmlns='http://www.w3.org/2000/svg'

                        p-id='6462'

                        width='200'

                        height='200'

                    >

                        <path

                            fill='white'

                            d='M889.3671875 697.51953124c2.10937499-4.21875001 4.21875001-8.6484375 6.328125-12.86718749 1.0546875-2.53125002 2.3203125-4.8515625 3.375-7.38281251 2.10937499-4.8515625 4.21875001-9.70312501 6.11718751-14.76562498 0.84375-2.10937499 1.6875-4.00781249 2.53125-6.1171875 2.7421875-6.96093751 5.0625-14.13281251 7.38281249-21.30468752 0.421875-1.0546875 0.6328125-2.3203125 1.05468749-3.37499998 1.8984375-6.11718751 3.5859375-12.234375 5.27343752-18.35156251 0.6328125-2.53125001 1.26562501-5.0625 1.68749998-7.59375 1.0546875-4.8515625 2.3203125-9.9140625 3.16406251-14.9765625 0.6328125-2.7421875 1.0546875-5.69531248 1.4765625-8.43750002 0.84375001-4.8515625 1.6875-9.703125 2.32031254-14.55468748 0.421875-2.953125 0.84375001-5.69531248 1.05468746-8.64843749 0.6328125-5.27343751 1.0546875-10.54687499 1.4765625-15.82031251l0.6328125-7.59375c0.421875-7.8046875 0.6328125-15.609375 0.63281249-23.625l0-6.5390625-0.21093749 0c-0.84375-55.26562501-12.65624999-108.2109375-33.53906249-156.30468751l-36.703125 16.03125c19.40625 45.140625 30.1640625 94.7109375 30.16406249 146.81250001 0 7.17187501-0.2109375 14.34375001-0.6328125 21.3046875-0.2109375 2.3203125-0.421875 4.64062501-0.42187501 6.74999998-0.421875 4.8515625-0.84375001 9.49218751-1.26562499 14.34375002-0.2109375 2.53125002-0.6328125 5.27343751-1.0546875 7.80468749-0.6328125 4.4296875-1.26562501 8.859375-2.109375 13.07812502-0.421875 2.53125002-0.84375001 5.2734375-1.4765625 7.80468748-0.84375 4.4296875-1.8984375 8.859375-2.953125 13.28906251-0.6328125 2.3203125-1.0546875 4.64062501-1.6875 6.96093749-1.26562501 5.2734375-2.7421875 10.54687499-4.4296875 15.8203125-0.421875 1.26562501-0.6328125 2.7421875-1.05468751 4.00781251-2.10937499 6.53906251-4.21875001 12.86718751-6.53906249 19.1953125-0.6328125 1.6875-1.4765625 3.5859375-2.10937501 5.2734375-1.6875 4.64062501-3.5859375 9.0703125-5.48437501 13.5-1.0546875 2.3203125-2.10937499 4.4296875-3.16406248 6.75-1.8984375 4.00781249-3.796875 7.80468751-5.6953125 11.60156252-62.64843753 123.39843751-191.953125 208.1953125-341.71875 208.19531249-210.7265625 0-381.79687502-168.11718751-381.796875-375.67968751C130.20312498 304.33203125 301.2734375 136.21484377 512 136.21484377l6.75 0L518.75 96.76953127 512 96.76953128C278.9140625 96.55859375 90.12500001 282.60546873 90.12500001 511.89453125c0 229.50000001 188.78906252 415.3359375 421.87499999 415.33593752 163.68750001 0 305.43749999-91.7578125 375.2578125-225.70312502l0.21093749 0c0.6328125-1.26562501 1.26562501-2.7421875 1.89843751-4.00781251z'

                            p-id='6463'

                        ></path>

                    </svg>

                    Submitting...

                </button>

            </div>
```

![](attachments/Pasted%20image%2020251207164947.png)

```tsx
            {/* animate-ping */}

            <div>

                {/* position all base on this span */}

                <span className='relative inline-flex group'>

                    <button

                        type='button'

                        className='py-2 px-4

                inline-flex gap-4 items-center

                shadow rounded-md

                bg-indigo-500 group-hover:bg-indigo-400

                transition ease-in-out duration-150

                text-white

                font-bold

                '

                    >

                        Transactions

                    </button>

                    <span

                        className='flex

                    -mt-1 -mr-1

                    h-3 w-3

                    absolute top-0 right-0

                    '

                    >

                        <span

                            className='

                            group-hover:animate-ping

                            absolute inline-flex

                        rounded-full

                        bg-sky-400 opacity-70

                        h-full w-full'

                        >

                            {/* dynamic */}

                        </span>

                        <span

                            className='

                        h-3 w-3

                        rounded-full

                        bg-sky-500 '

                        >

                            {/* fixed */}

                        </span>

                    </span>

                </span>

            </div>
```

![](attachments/Pasted%20image%2020251207165012.png)

```tsx
            {/* animate-pulse */}

            <div

                className='

            animate-pulse

            bg-slate-500 py-10 px-5 rounded-lg shadow-lg w-80'

            >

                <Skeleton />

            </div>

  

            {/* animate-bounce */}

            <div

                className='

                animate-bounce

            flex items-center justify-center

            bg-slate-600 p-2 w-10 h-10 shadow-lg rounded-full'

            >

                <svg

                    viewBox='0 0 1024 1024'

                    version='1.1'

                    xmlns='http://www.w3.org/2000/svg'

                    p-id='12399'

                    width='200'

                    height='200'

                >

                    <path

                        fill='white'

                        d='M690 405h-46.9c-10.2 0-19.9 4.9-25.9 13.2L512 563.6 406.8 418.2c-6-8.3-15.6-13.2-25.9-13.2H334c-6.5 0-10.3 7.4-6.5 12.7l178 246c3.2 4.4 9.7 4.4 12.9 0l178-246c3.9-5.3 0.1-12.7-6.4-12.7z'

                        p-id='12400'

                    ></path>

                    <path

                        fill='white'

                        d='M512 64C264.6 64 64 264.6 64 512s200.6 448 448 448 448-200.6 448-448S759.4 64 512 64z m0 820c-205.4 0-372-166.6-372-372s166.6-372 372-372 372 166.6 372 372-166.6 372-372 372z'

                        p-id='12401'

                    ></path>

                </svg>

            </div>
```

```tsx
const Skeleton = () => {

    return (

        <div className='flex space-x-4'>

            <div className='rounded-full bg-slate-200 dark:bg-slate-700 h-14 w-14'></div>

            <div className='flex-1 space-y-6 py-1'>

                <div className='h-2 bg-slate-200 dark:bg-slate-700 rounded'></div>

                <div className='space-y-3'>

                    <div className='grid grid-cols-3 gap-4'>

                        <div className='h-2 bg-slate-200 dark:bg-slate-700 rounded col-span-2'></div>

                        <div className='h-2 bg-slate-200 dark:bg-slate-700 rounded col-span-1'></div>

                    </div>

                    <div className='h-2 bg-slate-200 dark:bg-slate-700 rounded'></div>

                </div>

            </div>

        </div>

    );

};
```

![](attachments/Pasted%20image%2020251207165038.png)


